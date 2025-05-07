---
title: 遊戲怪物名稱搜尋 Line Chatbot
tags: [Line Chatbot]
layout: single
date: 2020-03-04
toc: true
toc_sticky: true

---

## 1.建立 怪物 Google 表單(作為資料庫)
    檔案>發佈到網路，選擇.CSV路徑即可使用
![](https://i.imgur.com/CbvAozM.png)

## 2.建立 Line Chatbot
    於 Line Developer 建立 Chatbot，並取得 LINE_ACCESS_TOKEN (Assertion Signing Key 
)
![](https://i.imgur.com/MOKoKfO.png)

## 3.啟用 Cloud Function
所使用到的範圍為 index.js、package.json 與 環境變數

![](https://i.imgur.com/nyIW8Jc.png)
#### 環境變數
    設定LINE_ACCESS_TOKEN
![](https://i.imgur.com/IJN7mEX.png)
#### package.json
    載入套件
``` json
{
  "name": "ro_game",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "dependencies": {
    "@line/bot-sdk": "^6.8.4",
    "axios": "^0.19.2",
    "lodash": "^4.17.15",
    "papaparse": "^5.1.1"
  }
}
```
#### index.js
    主程式
``` javascript
const _ = require('lodash')
const Line = require('@line/bot-sdk')
const Papa = require('papaparse')
const axios = require('axios')
/* 取得LINE_ACCESS_TOKEN由環境變數設置 */
const client = new Line.Client({
  channelAccessToken: process.env.LINE_ACCESS_TOKEN
})

/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */

/* 進入點 main */
exports.main = async (req, res) => { 
  const events = req.body.events
  for (const event of events) {
    await exports.handleEvent(event, req)
  }
  res.status(200).send('OK')
}
/* 回傳Chatbot資訊 */
exports.handleEvent = async (event, req) => {
  try {
    if (_.get(event, 'message.type') !== 'text') throw new Error('請輸入文字')
    const monsters = await exports.getMonsters()
    const text = _.get(event, 'message.text')
    const monster = _.find(monsters, m => m.name === text)
    if (!monster) throw new Error('找不到這個怪物')
    await client.replyMessage(event.replyToken, exports.renderMonster(monster))
  } catch (err) {
    console.log(err)
    await client.replyMessage(event.replyToken, {
      type: 'text',
      text: err.message
    })
  }
}
/* 怪物資料路徑(google表單.csv) */
exports.getMonsters = async () => {
  const CSVURL =
    'https://docs.google.com/spreadsheets/d/e/2PACX-1vQUGDJlinWJ4rkHyakRopU0fbOGniKO_2AmcvT4tlCWMl-DiYsG4kB_OneiQ6xzzxqhAQMj6BA4UvdR/pub?gid=0&single=true&output=csv'
  return await exports.getCsv(CSVURL)
}
/* 取得怪物資料(csv)並轉為csv */
exports.getCsv = async url => {
  url = new URL(url)
  url.searchParams.set('cachebust', _.floor(new Date() / 3e4))
  const csv = _.trim(_.get(await axios.get(url.href), 'data'))
  return _.get(
    Papa.parse(csv, {
      encoding: 'utf8',
      header: true
    }),
    'data',
    []
  )
}
/* chatbot渲染資料 */
exports.renderMonster = monster => ({
  type: 'flex',
  altText: monster.name,
  contents: {
    type: 'bubble',
    header: {
      type: 'box',
      layout: 'horizontal',
      contents: [
        {
          type: 'image',
          url: monster.img,
          flex: 0,
          size: 'sm'
        },
        {
          type: 'box',
          layout: 'vertical',
          contents: [
            {
              type: 'text',
              text: monster.name,
              size: 'xl',
              weight: 'bold',
              align: 'end',
              flex: 1,
              gravity: 'bottom',
              wrap: true,
              color: '#ffffff'
            },
            {
              type: 'text',
              text: monster.level,
              align: 'end',
              flex: 1,
              gravity: 'center',
              size: 'xl',
              color: '#ffffff'
            }
          ]
        }
      ]
    },
    body: {
      type: 'box',
      layout: 'vertical',
      contents: [
        {
          type: 'box',
          layout: 'horizontal',
          contents: [
            {
              type: 'text',
              text: '屬性',
              flex: 0,
              color: '#999999'
            },
            {
              type: 'text',
              text: monster.attr,
              align: 'end'
            }
          ]
        },
        {
          type: 'box',
          layout: 'horizontal',
          contents: [
            {
              type: 'text',
              text: 'HP',
              flex: 0,
              color: '#999999'
            },
            {
              type: 'text',
              text: monster.hp,
              align: 'end'
            }
          ]
        },
        {
          type: 'box',
          layout: 'horizontal',
          contents: [
            {
              type: 'text',
              text: 'BASE',
              flex: 0,
              color: '#999999'
            },
            {
              type: 'text',
              text: monster.base,
              align: 'end'
            }
          ]
        },
        {
          type: 'box',
          layout: 'horizontal',
          contents: [
            {
              type: 'text',
              text: 'JOB',
              flex: 0,
              color: '#999999'
            },
            {
              type: 'text',
              text: monster.job,
              align: 'end'
            }
          ]
        }
      ],
      spacing: 'md'
    },
    styles: {
      header: {
        backgroundColor: '#4f4f47'
      }
    }
  }
})

```