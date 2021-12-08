# OMERO @Crick (kenneth.ho[at]crick.ac.uk)

Date: 7 Dec 2021

* Crick's OMERO 
  * Crick has some 120 groups and some 1500 research staffs in a single site
  * OMERO Plus from Glencoe
  * 2 instances (1 production, 1 testing)
        * VM: 12 cores, 64GB ram, 120TB quota.
  * Separate configurations!!!   **(Don't do that!)**
  * Not Ansible (<u>work in progress</u>)
  * No high availability (<u>work in progress</u>)
---
<!-- .slide: data-state="ome_theme" -->
  * Uses Single-Sign-On (SSO)
    * <font color=blue> a pain to register new users
    * But easier to manage when people leave.</font>
* Use network files (Active Directory)
  * Recommend In-place import for our users
  * But no auto-import yet (<u>work in progress</u>)
  * <font color=blue>a pain to setup in-place import</font>
* External access URL for collaborations
* No Public User yet (i.e. no public website)
* AI/ML created pipelines for OMERO
---
<!-- .slide: data-state="ome_theme" -->
#### Current challenges
* QuPath ROI write back - SSL certificate probl. 
* Ansible/high availability/more instances for dev 
* Trouble using "*omero duplicate*" to external shared group when images are linked.
* Reading in sparse wells
* Users want *Maximum Intensity Projection*
* Transfer images between instances
* Commissioned Tape Backup option (Glencoe)