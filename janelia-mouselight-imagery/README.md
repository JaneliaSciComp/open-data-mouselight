# open-data-mouselight
MouseLight Gen1 Imagery hosted on AWS Open Data 

This bucket contains files for MouseLight's AWS Open Data.

## Implementation notes

* The Markdown used in this repo contains footnotes, which are [not supported by Github](https://github.com/github/markup/issues/498), so they will not render correctly in the Github preview. The actual publication target for these README's is [Quilt](https://open.quiltdata.com/b/janelia-mouselight-imagery) which does support footnotes. 

## Bucket structure

Files are organized by type and date:

* Root
    * images
        * `<date>` - each date represents an individual brain
            * default.0.tif - a TIFF format file containing single channel of entire image in low resolution used for 2-D viewer
            * default.1.tif - a TIFF format file containing single channel of entire image in low resolution used for 2-D viewer
            * ktx - texture files for Horta 3D viewer
                * `<number, 1-8>`
                    * `<number, 1-8>` (this structure of prefixes will continue for up to 7 levels)
                    * block_8_xy_`<number, 1-8>`.ktx - KTX format file containing actual image
                * block_8_xy_.ktx - KTX format file ...
            * tilebase.cache.yml - a YML format file containing spatial index for tiles
            * transform.txt - a text file containing origin, scaling, and number or levels in octree
    * registration
        * `<date>`
            * `<date>`.horta.yml - YML format file containing spatial index
            * `<date>`.nrrd - NRRD format file - a downsampled (monolitic) version of the imaged volume used for registration. The highest resolution (level) is matched to the 10um (isotropic) voxel size of the CCF.
            * `<date>`.yml - YML format file - file containing the information paths of original TIFF files, control points, barycentric transforms, etc._ required to stitch the individual tiles into a coherent volume. It is used by the render to generate the TIFF octree (Horta2D). If the workstation ever needs to access the paths of the original (raw) imagery, it does so by querying this file.
            * HortaObj
                * `<brain region>`_`<brain area ID>`.obj - multiple OBJ files (one per brain region) containing meshes. These are the CCF neuropil meshes "back-registered" into sample space (i.e, imaged samples).
            * Transform.`<date>`.h5 - - H5J format file. Contains the displacement fields required to transform (register) the sample into CCF space.
            * Transformed_`<date>`.nrrd - NRRD format file - this is the registered result: i.e, the transformed nrrd registered into the Allen CCF.
    * segmentation
        * `<date>` - SWC format neuron fragments generated during machine learning - structures vary
    * tracings
        * Finished_Neurons - internal (transient) version of tracings
            * `<date>`
                * `<fluorophore color>`-`<number>`
                * `<date>`_`<fluorophore color>`-`<number>`_`<annotator initials>`.swc - SWC format file
                * `<date>`_`<fluorophore color>`-`<number>`_`<annotator initials>`.swc - SWC format file
                * `<date>`_`<fluorophore color>`-`<number>`_dendrites.swc - SWC format file
                * consensus
                    * `<date>`_`<fluorophore color>`-`<number>`_base.swc - SWC format file
                    * `<date>`_`<fluorophore color>`-`<number>`_consensus.swc - SWC format file
                    * `<annotator initials>`_uni.swc - SWC format file
                    * Backup
                        * `<date>`_`<fluorophore color>`-`<number>`_consensus.swc - SWC format file
                    * `<annotator initials>`_uni.swc - SWC format file - individual annotator tracing
        * tracing_complete - this prefix contains files shown on Workstation
            * `<date>`
                * `<fluorophore color>`-`<number>`
                    * base.swc - SWC format file - annotator consensus
                    * consensus.swc - SWC format file of axon
                    * dendrite.swc - SWC format file of dendrite
                    * soma.txt - text format file containing soma location
                    * somaLoc.png - PNG format file
                    * somaOnt.png - PNG format file
                    * Thumbs.db
                    * uni1.swc - SWC format file - individual annotator tracing not in base
                    * uni2.swc - SWC format file - individual annotator tracing not in base
