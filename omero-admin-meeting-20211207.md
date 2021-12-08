# OMERO-admin meeting
## 7th December 2021

**Date/time:** 7 Dec 2021, 15:00 GMT (7h Pacific, 10h East, 15h UK, 16h Central Europe, 24h Japan)
**Location:** Online meeting via Zoom

Note: This Zoom meeting is being recorded for those who can't attend, if you don't want to be recorded, please let us know, we will turn that off by request.


* **Agenda**
  * Crib Talks
    * Introduce yourself
    * Short talk (3-5 minutes) on your facility
  * Transfer between OMERO instances
  * Free discussion/help desk


* Live notes at [Hackmd](https://hackmd.io/@UQQhmNEGSjGnTBxMsQkE5w/HyFun16YY/edit)

* [Video recording](https://crick.zoom.us/rec/share/Gsbm268NTJmVBrHjWwWPwft07WM_awjI55IT1l3HJjbHuZUU1ztDFpB3DHF1F8xb.iIS0k5lv5iOOQgas)
    * Passcode: j.xwXT.7

Notes:

* Erick and Dave Mellert work at The Jackson Laboratory, doing a lot of automation and admin work at a medium-sized OMERO instance. Eric is currently helping them on file formats issues and moving their public OMERO instance to the cloud.
* Ken work at The Francis Crick Institute in London. He used to work at RIKEN in Japan running OMERO as a public repositiory and joined Crick back in February this year.  Slides on [Crick OMERO](https://github.com/DrKenHo-crick/omero-admin-meeting/blob/main/crickomero-202111207.md)
* Jeffrey (MIT) is starting to implement OMERO
* Judith is setting up for Montreal community and for Canada
* Tao and Ved (Alison North group at Rockefeller Univ.) are exploring and trying to setup OMERO for users at their imaging facility.
* Erick: Is a general "basics of setting up OMERO" tutorial/workshop a community need?
    * KH: Yes I think there is a need for that
* Michelle at Chapel Hill - a pilot project on OMERO, currently installed and maintained by SOM IT, direct upload, uploading large files and processing. IT is evaluating for long term sustainabile project. Also a test local test instance of Omero with the Glencoe CellProfiler pipeline purchased.
* Kasia (Chapel Hill) bioimage analyst learning OMERO
* Mark (Goldfinch Bio) runs OMERO login from AD. 1 instance on AWS, data stored in S3 with AWS file gateway to provide filesystem for in-place import. Using docker-compose to manage 3 docker containers, omero-server, omero-web and ngnix_ssl. Some automation of data import from instruments. Next goal is to connect analysis tools to Omero to get real value from the image data.
* Allan (Harvard Medical School), along with Beth & Safet, 2 primarly instances, 1 production, 1 old Columbus that they don't like. 380TB images today. Find a way to archive them. Auto-ingestion of special instruments. 
* Arne (Life Imaging Center, Freiburg, Germany), only a test instance of omero, but nobody uses it so far! Will set up an omero instance for QUAREP-LiMi with 10 TB storage.
* Peter (Cologne) 2016 OMERO, 280 active users. 20TB of storage. PathViewer from Glencoe. Try to get users to annotate metadata. How to account for file quota.
* Niraj works with Peter.
* Jens (Muenster) - medium size OMERO, 300 core users, 10 TB of data. No inplace-upload. 2 instances of OMERO, 1 live, 1 test. Public access possible to the live server. Use of .iviewer/.figure/.parade/.OpenLink/.scripts. Work in progress: provide customized upload/annotation scripts/templates. Publication option with associated DOI is on the way. Struggling with metadata handling via Python.
* Damir (Portland Oregon), open-source production OMERO's since 2013, now also an institutional OMERO Plus instance. Challenges with running a public instance on AWS.
* Susanne (Osnabrueck), OMERO since 2016, 20 working group, 250 users, 120 TB of data. Working on extension and plugin, fileserver with external users.
* Rohola (Leiden U) some happy users, same issue with metadata.
* Laura Cooper (CAMDU, Warwick), archiving. automatic importing setup on quite a few microscopes. Challenge to get people using it. Covid19 help for remote access using web browser. 
* Anna (HHU Duesseldorf), core facility, including EM, not lightsheet data, 3 OMERO instances, 1 production, 1 test, 1 public. Public is not published yet because they struggle to transfer from private instances to public instances. HCS data more and more. Metadata import and convince people to use OMERO. Use it for teaching. 
* Pierre - not a big lab, 150 people in the lab. Work on OMERO for 10 years. 38 TB. Mainly using OMERO for image processing. Users don't use annotation much. Very slow uptakes. 


Topics:

Tranfering data
* Erick: How to do it such that we can preserve all the metadata?
* Erick can tranfer pixel data but not metadata and not if it is in_place import. 
* Erick: They was thinking of getting all the metadata in json files and the transfer will be image files and json files.
* Josh (OME) in image.sc suggested that we should co-ordinate to develop a solution in JSON-LD, i.e. RDF form. 
* Ken: It maybe easier to find simple solution that will solve some of the simple cases.
* Erick/Dave: They have already done something on tag and annotation transfer. 
* Rohola: They have already work with Josh on metadata to JOSN-LD. Roryo Kobayashi has already done that but not complete. 
* Dave: OME-Zarr format, metadata in JSON-LD

How to convince users to use metadata?
* Mark: How to get users to use not json but excel to input metadata?
* Dave: 2 options: 
    * 1. They give them excel file and let them fill that in. Basically it is a Map annotation, i.e. key-value pair. 
    * 2. Jackson uses LIMS to sync OMERO to link and import metadata.
* Judith: introduce users to use MicoMeta app. In the future it will be a great tool for populating meta to images.
* Dave: asked about the MicroMeta app.
* Damir: MicroMeta app provides a nice user interface and implements the new proposed extension of the OME-XML  Metadata model. See: https://www.nature.com/articles/s41592-021-01315-z for details and https://wu-bimac.github.io/MicroMetaApp.github.io/
 
**Action to do:**
We think a "basics of setting up OMERO" tutorial/workshop is needed for the community - we need to liase with OME as they are much better to recommend how to setup OMERO servers.

Jeffrey: what hardware should I buy?
Erick/Laura: 4 core 8GB machine.
Mark: Has a diagram on using AWS/1 EC2 instance, 32GB ram, S3 bucket. 

Peter: wants to test load his OMERO server
Dave: has a test script that uses Ezomero will hammer the server writing pixel and file attachment seem to kill the server and not concurrent users. https://github.com/TheJacksonLaboratory/ezomero

Ken: How to import images from Harmony/Phoenix?
Allan: Glencoe said that it was no go and Perkin wanted to sell him a different product.
Erick: Harmony has to use Export, that is only way to import it.
Dave: Harmony exports and convert that to ome-zarr, then link omero to it. That works great for analysing and accessing pixel level, etc.

Allan: micro-services split up the functionality but omero.web server can still be a bottleneck.

Jeffrey: Are we moving to convert everything to ome-zarr?
Erick: original files are retained for references but ome-zarr is used for analysis and viewing, etc.
Eric: We are in the transistion period but the future maybe quite different.



Attendees:

Name, Affiliation, contact@image.sc
1. Ken Ho, Francis Crick, @ken.ho
2. Erick Ratamero, The Jackson Laboratory, @erickratamero
3. Arne Fallisch, Life Imaging Center
4. Dave Mellert, The Jackson Laboratory, @mellertd
5. Judith Lacoste, MIA Cellavie Inc, for Claire Brown, Thomas Stroh (BINA, Canada BioImaging)
6. Eric Perlman, Yikes LLC (with The Jackson Laboratory), @perlman
7. Jeffrey Kuhn, Koch Inst, MIT
8. Ved Sharma, Rockefeller University, @vedsharma
9. Michelle Itano, University of North Carolina, @UNC_NMC
10. Susanne Kunis, University of Osnabrueck, @sukunis 
11. Tao Tong, The Rockefeller University, @ttong2046
12. Anna Hamacher, University of Duesseldorf, @ahamacher
13. Laura Cooper, CAMDU, University of Warwick, @Laura190
14. Peter Zentis, CECAD Koeln, @Peter.Zentis
15. Niraj Kandpal, CECAD Koeln,
16. Damir Sudar, Quantitative Imaging Systems LLC & Oregon Health and Science University, @dsudar 
17. Pierre Pouchin, , @pierre.pouchin
18. Jens Wendt, WWU Muenster, 
19. Mark Duggan, Goldfinch Bio,
20. Allan J Harris, Harvard Medical School,@Allan_Harris
21. Beth Beighlie,Harvard Medical School,@b2ool
22. Kasia Kedziora, UNC, @Kasia_Kedziora 
23. Safet Berberi,Harvard Medical School , 
