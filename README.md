# Overview

* [Privacy policy](https://xendiz.com/privacy-policy)
* [Terms of use](https://xendiz.com/terms-of-use)

# Xendiz DSP
* [API](./dsp/api)
  * [Overview](./dsp/api)
  * [Auth](./dsp/api#auth)
  * [Dashboard](./dsp/api#dashboard)
    * [List top os](./dsp/api#top-os)
    * [List top geo](./dsp/api#top-geo)
    * [List top apps](./dsp/api#top-apps)
    * [List top spend](./dsp/api#top-spend)
  * [Manage accounts](./dsp/api#accounts)
    * [Get account info](./dsp/api#get)
    * [Create new account](./dsp/api#create)
    * [Update account info](./dsp/api#update)
  * [Manage transactions](./dsp/api#accounts-transactions)
    * [Get account transactions list](./dsp/api#list)
  * [Manage campaigns](./dsp/api#campaigns)
    * [Get account's campaigns list](./dsp/api#list-1)
    * [Get account's campaigns tiny list](./dsp/api#tiny-list)
    * [Enable campaign](./dsp/api#enable)
    * [Disable campaign](./dsp/api#disable)
    * [Get campaign info](./dsp/api#get-1)
    * [Get linked creatives list for campaign](./dsp/api#creatives-list)
    * [Create new campaign](./dsp/api#create-1)
    * [Create campaign's copy](./dsp/api#make-copy)
    * [Update campaign](./dsp/api#update-1)
    * [Archive campaign](./dsp/api#archive)
    * [Unarchive campaign](./dsp/api#unarchive)
    * [Link creatives to campaign](./dsp/api#link)
    * [Unlink creatives from campaign](./dsp/api#unlink)
  * [Manage creatives](./dsp/api#creatives)
    * [Get account's creatives list](./dsp/api#list-2)
    * [Get account's creatives tiny list](./dsp/api#tiny-list-1)
    * [Get creative info](./dsp/api#get-2)
    * [Create new tag creative](./dsp/api#create-tag)
    * [Create new banner creative](./dsp/api#create-banner)
    * [Create new video creative](./dsp/api#create-video)
    * [Update tag creative](./dsp/api#update-2)
    * [Update banner](./dsp/api#update-banner)
    * [Update video](./dsp/api#update-video)
    * [Disable creative](./dsp/api#disable-1)
    * [Archive creative](./dsp/api#archive-1)
    * [Unarchive creative](./dsp/api#unarchive-1)
    * [Delete creative](./dsp/api#delete)
    * [Link creative to campaigns](./dsp/api#link-1)
    * [Unlink creative from campaigns](./dsp/api#unlink-1)
  * [User lists management](./dsp/api#lists)
    * [Get all lists](./dsp/api#get-all-account-lists)
    * [Create new list](./dsp/api#create-new-list)
    * [Work with list in bulk](./dsp/api#bulk-work)
    * [Update list name](./dsp/api#update-list)
    * [Delete list](./dsp/api#delete-list)
    * [Delete list entries](./dsp/api#delete-entry)
  * Availables
    * [OS](./dsp/api#available-os)
    * [Creative size](./dsp/api#available-sizes)
    * [ISP](./dsp/api#available-isp)
    * [City](./dsp/api#available-cities)
  * Reports
    * [Financial](./dsp/api#financial)
    * [Custom](./dsp/api#custom-report)
    * [Inventory Overview](./dsp/api#inventory-overview)
* [Web UI]()
* Integration
  * [FAQ](./dsp/integration/faq.md)
  * [Macros list](./dsp/integration/macros.md)

# Xendiz Marketplace
* [Cookie sync](./marketplace/cookie_sync)
  * [SSP](./marketplace/cookie_sync#cookie-syncing-with-xendiz-ssp)
  * [DSP](./marketplace/cookie_sync#cookie-syncing-with-xendiz-dsp)
* [API](./marketplace/api)
  * [SSP API](./marketplace/api/ssp)
    * [Overview](./marketplace/api/ssp#overview)
    * [Profile](./marketplace/api/ssp#profile-api)
      * [Company SSP endpoints](./marketplace/api/ssp#company-ssp-endpoints)
      * [SSP endpoint details](./marketplace/api/ssp#ssp-endpoint-details)
      * [Block creative](./marketplace/api/ssp#block-creative)
      * [Unblock creative](./marketplace/api/ssp#unblock-creative)
    * [Financial](./marketplace/api/ssp#financial-api)
    * [Custom report](./marketplace/api/ssp#custom-report)
  * [DSP API](./marketplace/api/dsp)
    * [Overview](./marketplace/api/dsp#overview)
    * [Profile](./marketplace/api/dsp#profile-api)
      * [Company DSP endpoints](./marketplace/api/dsp#company-dsp-endpoints) 
      * [DSP endpoint details](./marketplace/api/dsp#dsp-endpoint-details)
      * [Add item to block list](./marketplace/api/dsp#add-items-to-block-list)
      * [Remove item from block list](./marketplace/api/dsp#remove-items-from-block-list)
      * [DSP campaigns target](./marketplace/api/dsp#dsp-campaigns-target)
      * [Add DSP campaign target](./marketplace/api/dsp#add-dsp-campaign-target)
      * [Update DSP campaign](./marketplace/api/dsp#update-dsp-campaign)
      * [Delete DSP campaign target](./marketplace/api/dsp#delete-dsp-campaign-target)
      * [Change DSP endpoint URL](./marketplace/api/dsp#change-dsp-endpoint-url)
    * [Financial](./marketplace/api/dsp#financial-api)
    * [Detailed](./marketplace/api/dsp#detailed-reports-api)
      * [Campaign report](./marketplace/api/dsp#campaign-report)
      * [Creative report](./marketplace/api/dsp#creative-report)
      * [Domain list](./marketplace/api/dsp#domain-list)
      * [Bundle list](./marketplace/api/dsp#bundle-list)
      * [Specific domain report](./marketplace/api/dsp#specific-domain-report)
      * [Specific bundle report](./marketplace/api/dsp#specific-bundle-report)
      * [OS report](./marketplace/api/dsp#os-report)
      * [Geo report](./marketplace/api/dsp#geo-report)
      * [Users report](./marketplace/api/dsp#user-report)
      * [Custom report](./marketplace/api/dsp#custom-report)
  * [Trends API](./marketplace/api/trends)
    * [Overview](./marketplace/api/trends#overview)
    * [Applications](./marketplace/api/trends#applications)
    * [Sites](./marketplace/api/trends#sites)
    * [Formats](./marketplace/api/trends#formats)
    * [Device](./marketplace/api/trends#device)
* Integration
  * Glossary
  * DSP
    * Overview
    * Required fields
    * User matching
    * Discrepancies
    * Examples
  * SSP
    * Overview
    * User matching
    * Discrepancies 
    * Examples
