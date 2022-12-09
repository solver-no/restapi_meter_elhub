# restapi_meter_elhub
An easy to use REST API for Elhub metering data. The API also offers Nordpool's spotprices and grid tarifs and calcaulations.
For meters with an installed HAN adapter (Zohm HAN adapter, Tibber Pulse, etc) the API will provide realtime data as well.

As a part of the Norwegian https://www.stromradar.no project we created an easy to use REST API to retrieve metering values from the Norwegian ELHUB database.

Currently Elhub does not have a REST API.
* Read this link https://elhub.no/om-elhub/elhub-for-sluttbruker/min-side/#1633520149474-ab6c8c3a-333e and search for API.
* In English https://elhub.no/en/about-elhub/elhub-for-the-end-user/ (does not contain the FAQ though)

Zohm AS, developers of https://www.stromradar.no have made an easy  self service REST API to retrieve metering values for all Norwegian meters.

The API is published here: https://api.zohm.no ad https://api365.zohm.no

The APIs are more or less 100% identical, and usage depends on which ID provider you want to use.

If you want us to issue an API user (similar to cliend id / secret) you would need to send me an e-mail at support@zohm.no. With API users you should use https://api.zohm.no and get a bearer token at the /api/token endpoint (https://api.zohm.no/api/token)  

If you want to use Microsoft Office 365 IDs (work or school account), aka Azure AD accounts you would use https://api365.zohm.no
It might be that you want to login with your Office 365 ID first on https://portal.zohm.no to verify that your account can be used if your Administrator has restricted your user. 

The Zohm API has a comprehensive access and security model based on the self service Solver API (made by the developers behind SolverApp - https://www.solver.no)

You can test to retrieve our developers metering values as we have made these meter values public.

1) log in to https://admin.zohm.no with you Office 365 ID, click settings and grab your bearer token.
2) Use Postman and test the endpoints

    a) https://api365.zohm.no/api/Object/UserObjects to retrieve a list of meters you have access to. This list will probably be empty as you do not have any explicit access to any meters.

    b) https://api365.zohm.no/api/Object/UserObject/Search/A to search for meters made public. The "A" is just to initiate the search. You would probably get some of our developers home meters (Martin Vannkunsten and Dag's Meter). Grab the ObjectIDs, e.g 48 for "Dag's meter". Dag's meter has an installed HAN adapter, but object ID 47 "Martin Vannkunsten" only has values from Elhub.

    c) https://api365.zohm.no/api/Zohm002/MeteringPoint/Overview/48 to get an overview of the meteringpoint

    d) https://api365.zohm.no/api/Zohm002/MeteringPoint/Cost?objectId=47&fromDate=2022-12-01&toDate=2022-12-09&aggregationType=hour to get all meter values from a given range in hour resolution. We support year, month, day and hour resolution currently but will soon have drilldown on hours as well.

    e) For meters with a HAN adapter provided the https://api365.zohm.no/api/Zohm002/MeteringPoint/Cost?objectId=47&fromDate=2022-12-09&toDate=2022-12-09&aggregationType=hour on current date will update last hour value in real time.

    f) https://api365.zohm.no/api/Zohm002/MeteringPoint/GridCost?objectId=48&fromDate=2022-12-01&toDate=2022-12-09&aggregationType=day to get the grid cost for the given date range.

    g) https://api365.zohm.no/api/Zohm002/MeteringPoint/spotprice?objectId=47&fromDate=2022-12-01&toDate=2022-12-09&aggregationType=hour to get NordPool's spotprices for the given meteringpint
    
    h) https://api365.zohm.no/api/Zohm002/MeteringPoint/ETChart?objectId=48&fromDate=2022-12-01&toDate=2022-12-09&aggregationType=day&feltTemperature=false to get a ETChart values for the given meter and date range. 


To fully use and understand the API it would probably make sense to enroll some of your meters into the Zohm system (https://portal.zohm.no and API)
Please contact us at support@zohm.no.

Zohm Developers
