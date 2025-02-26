---
title: Template head models for forward volume conduction modeling
tags: [template, headmodel]
---

# Template head models for forward volume conduction modeling

Volume conduction models of the head are a necessary ingredient for source reconstruction. Sources are typically modeled as equivalent current dipoles (ECDs), i.e. point sources with a location and orientation. These sources produce an electrical current that flows through all surrounding tissue. The geometrical and conductive aspects of the tissue influence how the source becomes visible in the EEG or MEG.

{% include markup/warning %}
You can find the template head models included in FieldTrip [here](https://github.com/fieldtrip/fieldtrip/tree/master/template/headmodel).
{% include markup/end %}

## standard_bem

This file contains a standard Boundary Element Method volume conduction model of the head that can be used for EEG forward and inverse computations. The geometry is based on the "colin27" template that is described further down. The BEM model is expressed in MNI coordinates in mm.

The BEM model is based on the segmentation from [BrainWeb: Anatomical Model of Normal Brain](http://brainweb.bic.mni.mcgill.ca/brainweb/anatomic_normal.html). Its construction is detailled by Oostenveld et al. in [Clin Neurophysiol. 2003 Jul;114(7):1194-202](http://www.ncbi.nlm.nih.gov/pubmed/12842715); please cite this paper if you use this template volume conduction model in your analyses. A very similar BEM volume conduction model (based on the same template MRI) is described and validated by Fuchs et al. in [Clin Neurophysiol. 2002 May;113(5):702-12.](http://www.ncbi.nlm.nih.gov/pubmed/11976050).

Accompanying electrode positions according to the 10-20, the 10-10 and the 10-5 standards (with different naming schemes) can be found in the `template/electrode` directory.

## standard_mri

The original construction of the averaged "“colin27”" MRI is detailed in [here](https://www.bic.mni.mcgill.ca/ServicesAtlases/Colin27) and in the publication from Holmes et al. in [J Comput Assist Tomogr. 1998 Mar-Apr;22(2):324-33](http://www.ncbi.nlm.nih.gov/pubmed/9530404).

The relation of the "colin27" MRI to the Talairach-Tournoux atlas and to the MNI and SPM templates is described in detail [here](http://imaging.mrc-cbu.cam.ac.uk/imaging/MniTalairach). A small excerpt follows:

_One of the MNI lab members, Colin Holmes, was scanned 27 times, and
the scans were coregistered and averaged to create a very high
detail MRI dataset of one brain. This average was also matched to
the MNI305, to create the image known as "colin27". \[The colin27 image\] is used
in the MNI brainweb simulator. SPM96 used colin27 as its standard
template. \[...\] SPM96 and later contains a 2mm resolution copy of
the same image, in the canonical directory of the SPM distribution.
In SPM96 this is called T1 in later distributions it is called
single_subj_T1._

#### revision information

Up to r7413 (Jan 2013) the file content corresponded to the original anatomical MRI. From r7414 onwards the anatomical MRI was updated with private/volumeedit to remove the aliasing effect that resulted in the volume to contain segmentation-corrupting data very close to the top of the head.

As of August 23, 2018, the hdr-field has been removed from the data structures in standard_mri, and standard_seg. This was done because there was confusing information in these hdrs, which was inconsistent with the volumetric image (transformation matrices and fiducial locations).

## skin

This directory contains a triangulated high-resolution geometrical description of the skin surface. This skin surface is not used in the BEM model itself for computational reasons, but can be used for visualization. It is expressed in MNI coordinates in mm.

You can visualize it with

    >> skin = ft_read_headshape('standard_skin_14038.vol')

    skin =
       pnt: [14038x3 double]
       fid: [1x1 struct]
       tri: [28072x3 double]
      unit: 'mm'

    >> ft_plot_mesh(skin, 'edgecolor', 'none', 'facecolor', 'skin')
    >> camlight

{% include image src="/assets/img/template/headmodel/headmodel_skin.png" width="300" %}
