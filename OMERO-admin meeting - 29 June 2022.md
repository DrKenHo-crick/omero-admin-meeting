# OMERO-admin meeting - 29 June 2022

**Date/time:** 29 June 2021, 15:00 BST
**Location:** Online meeting via Zoom

Note: This Zoom meeting is being recorded for those who can't attend, if you don't want to be recorded, please let us know, we will turn that off by request.

Live notes on HackMD: https://hackmd.io/@UQQhmNEGSjGnTBxMsQkE5w/HkoWj0Kq9 

Zoom recording: https://crick.zoom.us/rec/share/Cil_BJLaOn4nGmi1-vczbJzGSKKN_O0X2R0NB0Z1Fdya9qgSH4L07Et7rCYEHT6n.-rJDCpPtmIQI53CM 

Passcode: =FO*6^Uw

* Participants:
Ken Ho (KH), Erick Ratemero (ER), Guillaume Gay (GG), Christian Schmidt (CS), Pierre Puchin (PP), Stephen Ogg(SO), Alice Kang (AK), Benjamin, Caterina Strambio De Castilla (CS), Damir Sudar (DS), Jens Wendt(JW), Josh Moore(JM), Judith Lacoste (JL), Kwasi Kwakwai (KK), Laura Cooper (LC), Lech Nieorda(LN),Luiz Gadlha(LG), Martin Hohmuth(MH), Michele Bortolomeazzi (MB), Moritz Hoevels(MH), nadia goue (ng), Niraj kandpal (Nk), Nour Larifi(NL), Peter Zentis(PZ), Simon Murray(SM), Susanne Kunis(SK), Sebastien Besson(SB), Tatiana Woller(TW), Tom Boissonnet(TB), Vasyl Vaskivskyi


* **Agenda**

* **Gulliaume Gay presentation**
    * Data from microscope normally need to be transferred to network storage and then to be imported into OMERO
    * Question: how to get the data out of microscope
    * Four main constraints
    * 1. user friendly or else people don't use it
    * 2. data to be transferred as quickly as possible
    * 3. Normally microscopes are used from 8am to 8pm.
    * 4. Big data and robostness and also friendly to admin.
    * Two main roles:
    * 1. Transport data and import at the same time 
 


    * Slides are now available
    Tools available:
    * 1. OMERO-insight
    * 2. OMERO-MS-Queue
    * 3. Robocopy
    * 4. pure CIFS
    * 5. Seafile/Nextcloud
    * 6. iRODS (not on slide)


    * import cli/script
    * omero inplace importer


JM Question: omero-insight is in maintenance mode and is not adding features. But if people are happy to use that, it can be moved out of maintenance mode. iRODS may well be one way forward.

ER: Jax does not do any data filtering. 
Use [globus](https://www.globus.org/data-transfer) or simple SMB drives. Has to have some annotation.


PP: Does anyone using omero-fs for automatic import?

ER: he doesn't aware or know anyone using that.

KH: We use in-place import and do not recommend using insight because users can access the original file from other proprietary software.

ER: We also use in-place import mainly.

JW: We mainly use insight  in fear of inplace import corrupting the db
SB: should not be a pb

ER: user can delete the data, not accessible any more

KH: user can only 'read', omero server owns all the image data file. However, if not set properly, users can delete, move their images, directories and causes errors with OMERO.

SK : robocopy used at Basel 
_we_ use omero insight & for big data import via omero web (server mounts the data ) user puts data on a specific directory in the directory of a specific username. For the moment it's synchronous but should be possible to make a job.

ER: we can classify in 2 big classes

1. user initiated (good)

2. not user initiated

MB: (DKFZ, Heidelberg) still at testing mixture of 1 and 2. (user drops the files into a share and starts the import from  dedicated image analysis computers ) and fully automated for specific instruments in Python. Do you do annotattion while importing?


ER: yes we do import and annotation from the spreadsheet together. To clarify, we're using ezomero, so annotation is technically a separate step to import because import happens in a separate CLI process, but they happen on the same orchestrating script

SB: in IDR (which is a slightly different workflow), we separate the import and the annotation steps

MB: Yes, same for us. Technically it is a separate CLI process, but it is all one python script and one job.

CS: pilot at UMas MedSchool the users saves data to a network drive on an analysis work station cron job on a set of folders + spreadsheet will also be tested in canada (in Java)

GG: How to normalize spreadsheet?

CS: fill in as much info as possible with controlled vocabulary
ER: we use a template w/o a controlled vocab. If issues we send a log file with errors to the user, the users fixes it 

Pierre Pouchin to Everyone (15:43)
Guillaume, hadn't you developed something to populate annotations?
Guillaume Gay to Everyone (15:44)
yes :) it needs work but it was a form filling website with queries to bioontology

Jens Wendt | Imaging Network Muenster to Everyone (15:45)
OMERO.forms?

Guillaume Gay to Everyone (15:45)
https://gitlab.in2p3.fr/fbi-data/cataloger

ER: Is there a consistent way to standarise import files and annotations together, be it josn-ld, etc.

JM: we need a model  of the import queue + prerequisites 
work form the community to say what standards

Jens Wendt | Imaging Network Muenster to Everyone (15:47)
I think the spectrum of annotation is just to broad to develop one general standard
Caterina Strambio De Castillia to Everyone (15:48)
In my opinion, there are sub-areas in the annotation “graph” that can be standardized while other things will be different per institution/lab

Sébastien Besson to Everyone (15:49)
import workflows

Guillaume Gay to Everyone (15:49)
maybe what can't be standardized should be designed with a template creation tool

Erick Ratamero (The Jackson Laboratory) (he/him) to Everyone (15:49)
I'm thinking the import/annotation process is not too far from what is done with transfer

KH: I am a bit skeptical that it is easy to fit everyone due to the IT infrastructure setup and constraint.

ER: maybe we cannot make it fit everyone, but if we can make something that satisfy 80% that would be good. Maybe a cli based solution would be flexible enough to cover most cases.

SB: even import can be split into sub-tasks 
JM: pre-processing (user-confirmation, add-annotation) / post-processing (annotate, generate-thumbnails, …) 

Sébastien Besson to Everyone (15:54)
that's where Jens concenrns kick back in!

Sébastien Besson to Everyone (15:55)
because you can really foobar the DB indeed

Josh Moore | OME to Everyone (15:57)
other YAML actions: convert, regions, deconvolve, adjust contrast, ....

JM: snakemake
ER: nextflow

JM: expand / speciffy bulk_import.yml
ER: could also have FileAnnotation & ROIs imported directly

SB: do we ensure data integrity before import?
Are post-processing steps inscope of that

CS: excel a good tool to make anotation (users like it), would be good to use a LIMS (Laboratory Image Management System)

ER: ≠ between metadata format & metadata standards 2 discussion

(JM, PP, ER) Good to have import depending on annotation so _have_ some user input.

VV: manual import with xlsx templates + validation step + web page to trigger import

ER: can you annotate images and not files (could be tricky) 

JM / SB: need to know image series number hard to know beforehand

Caterina Strambio De Castillia to Everyone (16:17)
I vote for insight, I am pretty sure multiple people will continue to use it in the foreseeable future…. Rebuilding it yes of course
but is it necessary to rebuild it?

Judith LACOSTE to Everyone (16:17)
+1 Caterina

Jens Wendt | Imaging Network Muenster to Everyone (16:18)
a web application would be nicer, removes the need to install something locally for the user

Josh Moore | OME to Everyone (16:18)
The stack: insight -> java gateway -> import candidates -> bioformats

Jens: no objection there. You just won't have Bio-Formats level validation during the upload.

KH to Everyone (16:19)
I am with Jen on web GUI instead of Java app on users' machines.

Guillaume Gay to Everyone (16:19)
+1 for web GUIs

Caterina Strambio De Castillia to Everyone (16:20)
Web GUI would work if it does everything that insight does

Josh Moore | OME to Everyone (16:20)
Then we need to compile Bio-Formats to WASM.

ER: we looked into tools to upload Tb of data, nothing goes all the way

SK: we tried with curl : create the script to the user that copy/paste it on the command line

### Points of action


- [ ] Think about Nextflow to cover server-side CLI workflow
- [ ] Client side: use insight? web application?
- [ ] omero-ms-queue "solves" the backend 
- [ ] Have a user survey 
- [ ] make a drawing (figma) and use to guide survey

