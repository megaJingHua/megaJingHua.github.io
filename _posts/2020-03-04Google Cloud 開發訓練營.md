---
title: Google Cloud 開發訓練營
tags: [Google Cloud]

---

# Google Cloud 開發訓練營
###### tags: `Google Cloud`

### [GDG Taichung](https://www.facebook.com/GDG.Taichung/)
( Google Developers group ) Facebook 社群。

### [Qwiklabs](https://www.qwiklabs.com/home?locale=en)
Qwiklabs 為雲端學習平台，教育用戶使用 Google Cloud 的所有產品，包括 Google Cloud Platform 與 G Suite。
[詳細課程內容：GCP Essentials
](https://google.qwiklabs.com/quests/23?qlcampaign=GCPUGTaipei-2346)

###### 資料來源：[Google買下學習平台Qwiklabs，要讓企業熟練使用Google Cloud](https://www.ithome.com.tw/news/109742)

### [Coursera](https://www.coursera.org/recommendations)
為雲端學習平台，可共享課程和專業證書。
[詳細課程內容：Google Cloud Platform Fundamentals: Core Infrastructure](https://www.coursera.org/learn/gcp-fundamentals)


## 📍 課程內容
1. GCP 主控台操作及資源管理
2. 建置虛擬機器與虛擬網路 (Compute Engine & VPC Networking)
3. 儲存空間與資料庫服務介紹 (Storage & Cloud SQL)
4. 容器服務與部署 (Kubernetes Engine)
5. 應用程式開發的 PaaS 服務 (App Engine & Cloud Functions)
6. 資料平台與機器學習服務 (Big Query, Machine Learning APIs)

## 📍 Google Cloud Platform ( GCP ) 主控台操作及資源管理
### Identity and Access Management ( 身分識別與訪問管理, IAM )
管理員可以授權哪些使用者可對特定資源進行操作，因此您可以完整掌控並清楚瞭解全局，以便集中管理雲端資源。
* Who：授權給誰?
* Can do what：可以做甚麼? ( primitive、editor、viewer、administrator、predefined )
###### 資料來源：[CLOUD IDENTITY & ACCESS MANAGEMENT](https://cloud.google.com/iam/)
### Resources < Projects < Folders
|Projects|||
|---|---|---|
Project ID |Globally unique Chosen |By you immutable|
Project Name| Need not be unique |Chosen by you mutable|
Project number |Globally unique assigned by GCP |Immutable|


## 📍建置虛擬機器與虛擬網路 (Compute Engine & VPC Networking)
[詳細課程內容：Creating a Virtual Machine](https://google.qwiklabs.com/focuses/3563?catalog_rank=%7B%22rank%22%3A2%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=1763048)
### VM
[ VM 規格價格介紹及初步架設教學](https://blog.gcp.expert/google-compute-engine-intro-demo/)
### CDN ( Content Delivery Network, 內容傳遞網路)
是一種在網路上傳輸的內容快取機制，透過不同全球不同節點佈有 CDN 服務，能夠有效降低內容傳輸的延遲，確保網站在世界各地讀取維持同等的速度。因此，CDN 具有加速網頁瀏覽、有效分流、高穩定性及高安全性等特質。
###### 資料來源：[Google也有CDN – Cloud CDN](https://blog.gcp.expert/cloud-cdn-intro/)
### VPC ( Virtual Private Cloud | Google Cloud, 虛擬私人雲端)
[Google cloud VPC](https://cloud.google.com/vpc/?hl=zh-tw)
### Comparing Compute Options
||Compute engine|Kubernetes engine|App engine flex|  App engine standard|Cloud functions|
|---|---|---|---|---|---|
|Service Model |IaaS| Hybrid| PaaS |PaaS| Serverless|
|Use cases |General computing workloads|Container-based wokloads|Web and mobile applications; container-based workloads|Web and mobile applications |Ephemeral functions respondint to events|
<-----Toward managed infrastructure_____________________Toward managed infrastructure----->
### Google VPC offers a suite of load-balancing option
|Global HTTP |Global SSL Proxy |Global TCP Proxy |Regional |Regional internal|
|---|---|---|---|---|
|Layer 7 load balancing based on load|Layer 4 load balancing of non-HTTPS SSL traffic base on the load| Layer4 load balancing of non-SSL TCP traffic| Load balancing of any traffic ( TCP, UDP )|Load balancing of traffic inside a VPC|
|Can route different URLs to different back ends|Supported on specific port numbers| Supported on specific port numbers| Supported on any port number| Use of the internal tiers of multi-layer applications|




## 📍儲存空間與資料庫服務介紹 (Storage & Cloud SQL)
### Comparing storage options: technical details
||Cloud Datastore|Bigtable|Cloud Storage|Cloud SQL|Cloud Spanner|BigQuary|
|---|---|---|---|---|---|---|
|Type|NoSQL document|NoSQL wide column|Blobstore|Relational SQL or QLTP|Relational SQL or OLTP| Relational SQL or OLAP| 
|Transactions|Yes|Single-row|No|Yes|Yes|No|
|Complex Queeries|No|No|No|Yes|Yes|Yes|
|Capacity|Terabytes+|Petabytes+|Petabytes+|Terabytes|Terabytes|Terabytes+|
|Unit Size|1MB/entity|~10MB/cell~100MB/row|5TB/object|Determined by DB engine|10240MiB/row|10MB/row|

### Choosing among Cloud Storage classes
||Multi-regional|Regional|Nearline|Coldline|
|---|---|---|---|---|
|Intended for data that is...|Most frequently accessed|Accessed frequently within a region|Accessed less than once a month|Accessed less than once a year|
|Availability SLA|99.95%|99.90%|99.00%|99.00%|
|Access APIs|Consistent APIs|Consistent APIs|Consistent APIs|Consistent APIs|
|Access time|Millisecond access|Millisecond access|Millisecond access|Millisecond access|
|Storage Price|▁▁▁▂▂▂|▃▃▃▅▅▅|▅▅▆▆▆▆|▇▇▇▇▇▇|
|Retrieval Price|▇▇▇▇▇▇|▆▆▆▆▅▅|▅▅▅▃▃▃|▂▂▂▁▁▁|
[Storage Classes](https://cloud.google.com/storage/docs/storage-classes)
[Buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)
[SQL](https://)


## 📍容器服務與部署 (Kubernetes Engine)
[詳細課程內容: Hello Node Kubernetes](https://google.qwiklabs.com/focuses/564?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=1763096)
[kubernetes](https://medium.com/@yicheng_/google-cloud-kubernetes-engine-%E4%BD%BF%E7%94%A8%E6%95%99%E5%AD%B8-1a500f4895b5)


## 📍應用程式開發的 PaaS 服務 (App Engine & Cloud Functions)
[詳細課程內容: App Engine: Qwik Start - Python](https://google.qwiklabs.com/focuses/1014?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=1763464)
### Example App Engine Standard Workflow - Web Applications
* Step1. Develop & test the web application locally.
* Step2. Use the SDK to deploy to App Engine.
![](https://i.imgur.com/8gmQLba.png)
* Step3. App Engine automatically scales & reliably serves your web application.


## 📍資料平台與機器學習服務 (Big Query, Machine Learning APIs)
[詳細課程內容：Google Cloud Platform Big Data and Machine Learning Fundamentals](https://www.coursera.org/learn/gcp-big-data-ml-fundamentals-fr)
[詳細課程內容: Using the BigQuery Web UI](https://google.qwiklabs.com/focuses/3616?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=1763614)













