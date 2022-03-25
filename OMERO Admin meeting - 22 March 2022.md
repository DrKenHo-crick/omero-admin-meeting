---
type: slides
---
# OMERO Admin meeting - 22 March 2022

Start time: 15:00 GMT
Current time is 14:50

Due to change in summer time in the US, there is some confusion on the time of this meeting.

It will start in around 10 mins from now.

See you soon

Ken


---

Date/time: 22 Marchh 2022, 15:00 GMT 

Location: Online meeting via Zoom

Note: This Zoom meeting is being recorded for those who can’t attend, if you don’t want to be recorded, please let us know, we will turn that off by request.

---

**Agenda**

- Crib Talks
- Introduce yourself
- Short talk (3-5 minutes) on your facility
- Transfer between OMERO instances
- Free discussion/help desk

- Live notes at Hackmd
  - [Hackmd](https://hackmd.io/3j-3PGFuT_q44z_Yhv0TDQ?both)

- [Zoom recording](https://crick.zoom.us/rec/share/h9dlyF-7xUwQv4KA_fDbGnNjcnlelxMaJ_EH3koJHpHuXS8LL6aBegearAEQ-xk.5oxQpYPdAWfIY_lr)
  - Passcode: #$NX!i9G

---
Notes:

Ken: Omero plus instance with aorund 60 active users and around 20TB of images. Some problem with high thread counts lately due to ms-image-region, working with Glencoe to resolve this.

Erick working for Jackson Lab. Providing software/hardware support for image analysis and data management, including an OMERO instance

Arne: working at installing OMERO for Quarep

Susanne: running OMERO since 2016, some web apps, some plugins

Jens: 200 users and around a dozen of active users at any time. Working on a publication workflow with DOIs, Streamlining annotations with Scripts, trying to push web-apps to the user(parade, crossfilter-parade, figure, etc.).

Felix: More than 600 active users.

Moritz: about 400 users. enlarge the ration of people using OMERO.

Michele: working with Felix, working with users on the pilot phase.

Hanka is also working with Michele and Felix. Working with annotation and to facilitate the use for external users.

Christian working with Susanne, Roland and others in the I3D:bio project (Information Infrastructure for BioImage Data), locally with Felix, Hanka and Michele (DKFZ, Heidelberg), and with Josh and others in the NFDI4BIOIMAGE initiative (https://nfdi4bioimage.de).

Damir - working close with Portland, Oregon - based Oregon Health & Science University where we support a number of OMERO instances. My company Quantitative Imaging, builds specialized image analysis software, currently focused on highly multiplex imaging with our QiTissue package: https://application.qitissue.com. Contact me if interested in trying it out.

Tom hasn't started yet and haven't used it yet. Joining the core facility in Düsseldorf in May (I3D:bio).

Pierre (admin for two local instances) developed tools for ImageJ and plugin tools for batch processing on OMERO.

Juidth from Montreal and work with Quraep WG4. Foster usage of OMERO, making images to be publically available. Interested in the naming condition of files, paths, key value pairs.

Roland coordinating QUAREP-LiMI and part of I3D:bio wants to initiate together with France RTmfm connecting MetroloJ_QC with OMERO for automated microscopy QC. 

Jeffrey runs the facility at MIT. Testing OMERO. Hoping to integrate with [Fairdom-SEEK](https://seek4science.org/)

Anna is omero admin providing new features for users.

Julia working with Susanne (I3D:bio). 

Stephen managing images for Canada! Now he is a Saudi, starting up again!

Josh started using OMERO in 2006! version 3.0!

Guillaume setting up omero for all [France BioImaging](https://france-bioimaging.org) nodes. Common setup detailed in here https://fbi-omero.os-bird.glicid.fr/ 


## On setting up OMERO

Josh: difficult to find one guideline fit all. But best to use ansible such that it is possible to share those work with others.

Erick: what should one be aware of, in terms of what software, hardware, etc instead of just digging into OMERO documentation.

Josh: best to come to OME meeting.

Ken's points
1. glencoe didn't support ansible script. However, it is managed by them, so no need to worry 😅. But ansible, dockerfile are good points to document the installation.
2. workshop for admin @ ome meeting? Josh: no capacity at present but they will look into it.
3. running out of /tmp/ **wiki entry**

Stephen: we should not worry about hardware and best to use online services.

Ken: difficult for research institutes to use subscription model as their funding is based on procurements.

Erick: OMERO doesn't use bucket so it can get expensive

Roland agrees with Ken that they cannot find it easy to use online services over procuring hardware.


## Erick introduction on his tools
- [ezomero](https://github.com/TheJacksonLaboratory/ezomero)
    - creating a layer to help using OMERO
- [jax-omero-transfer](https://github.com/TheJacksonLaboratory/jax-omero-transfer)
- [omero-cli-transfer](https://github.com/ome/omero-cli-transfer)
    - transfering between a private OMERO and a public facing OMERO where all the storages are separated.
    - He uses kubernetes instead of ansible.
    - Jens: can it be used for transfering from Columbus; Seb said that Erick code is based on version 5, while Columbus is based on version 4.
    - Anna: is namespace in mapannotations supported?; Erick: yes it is supported.
    - Best to use the CLI one than the python code above.
- jax-gcp-omero - currenly private but will be released soon.
- https://images-test.jax.org/
- using google cloud storage for publication data
- [docker-from-omero-poc](https://github.com/erickmartins/docker-from-omero-poc)

## OME team
Speaking of OMERO.web - https://www.openmicroscopy.org/2022/03/21/omero-web-5.14.0.html in case you missed it (OMERO.web on Django 3.2 LTS)
- no new features but only for security concern.
- highly recommend to upgrade.

Guillaume: what happens with IRODs and OMERO?
Josh: nothing much happen, but IRODs is quite active in getting that to work with OMERO, so it will happen, but at present Josh does not have one to test. The use case is driven by the University of North Carolina, Michelle as she has a use case and she has both IRODs and OMERO.

**OME Meeting will be in September, most likely in Dundee and in person only.**

Jeffrey asked about importing images, what is the recommended way to set that up.
https://forum.image.sc/t/inplace-importer-in-omero-script/27131

Update of Cellprofiler-OMERO plugin ongoing (Glencoe + Beth's team), probably **not** released within 6 months

## Next meeting in 3 months time. 
### Possible topics:
- Jens's publication workflow (if it is ready)
- Alex-rapp's [OMEROInplaceImporter](https://github.com/alex-rapp/omeroinplaceimporter)?
- others? 
---

Attendees:

Name, Affiliation, contact@image.sc
1. Ken Ho, Francis Crick, @ken.ho
2. Erick Ratamero, The Jackson Laboratory, @erickratamero
3. Jens Wendt, WWU Muenster Imaging Network, https://forum.image.sc/u/jenswendt/
4. Josh Moore, University of Dundee & German BioImaging, @joshmoore
5. Susanne Kunis, CellNanOs, University Osnabrueck, Germany, @sukunis
6. Jeffrey Kuhn, KI Microscopy Core Facility, MIT, Boston, @drjrkuhn
7. Damir Sudar, Quantitative Imaging Systems, @dsudar
8. Judith Lacoste, MIA Cellavie Inc, Montreal Canada, QUAREP-LiMi WG4, BINA QC DM, MicroMetaApp, McGill University Claire Brown and Thomas Stroh, Canada's National_OMERO, thanks to Steve OGG.
9. Roland Nitschke,Uni Freiburg, QUAREP-LiMi, I3d:bio, https://quarep.org/ 
10. Guillaume Gay, France BioImaging Montpellier, @glyg
11. Arne Fallisch,Uni Freiburg, QUAREP-LiMi, I3d:bio, https://quarep.org/
12. Steve Ogg, KAUST, @steveo
13. Anna Hamacher, CAi HHU Düsseldorf, @ahamacher
14. Tom Boissonnet, CAi HHU Düsseldorf
15. Michele Bortolomeazzi, DKFZ Heidelberg, @Michele_Bortolomeazz
16. Christian Schmidt, DKFZ Heidelberg, @SchmChris
17. Pierre Pouchin, , @pierre.pouchin