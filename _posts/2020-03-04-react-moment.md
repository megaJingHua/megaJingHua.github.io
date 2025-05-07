---
title: react-moment
tags: [React]
layout: single
date: 2020-03-04
toc: true
toc_sticky: true

---


## Installing
``` 
npm install --save moment react-moment
```
## Import
import the package into your project.
``` react
import React from 'react';
import Moment from 'react-moment';
 
export default class App extends React.Component {
    ...
}
```

## Example
react
``` react
import React  from 'react';
import Moment from 'react-moment';
 
export default class MyComponent extends React.Component {
    render() {
        return (
            const dateToFormat = '1976-04-19T12:59-0500';
            <Moment>{dateToFormat}</Moment> //1976-04-19 12:59
        );
    }
}
```
javascript
``` javascript
let date = '1976-04-19T12:59-0500';
let newDate = moment(data).format('YYYY-MM-DD HH:mm');
console.log(newDate) //1976-04-19 12:59
```

## Format
react
``` react
<Moment format="YYYY/MM/DD">
    1976-04-19T12:59-0500 //1976/04/19
</Moment>
```
javascript
``` javascript
let date = '1976-04-19T12:59-0500';
let newDate = moment(data).format('YYYY/MM/DD');
console.log(newDate) //1976/04/19
```
## Add and Subtract
react
``` react
import React  from 'react';
import Moment from 'react-moment';
 
export default class MyComponent extends React.Component {
    render() {
        const date = new Date();
 
        return (
            <div>
                <Moment add={{ hours: 12 }}>{date}</Moment>
                <Moment add={{ days: 1, hours: 12 }}>{date}</Moment>
                <Moment subtract={{ hours: 12 }}>{date}</Moment>
                <Moment subtract={{ days: 1, hours: 12 }}>{date}</Moment>
            </div>
        );
    }
}
```
javascript 
``` javascript
let addTime = {m: 2, d: 1, h: 3, M: 0};
let date = '1976-04-19T12:59-0500';
let newTime = moment(date).add(addTime).format('YYYY-MM-DD HH:mm');
console.log(newTime)//1976-06-20 15:59
```
###### 資料來源：[react-moment](https://www.npmjs.com/package/react-moment#add-and-subtract)