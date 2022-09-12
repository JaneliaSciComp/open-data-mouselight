## Introduction
Amazon provides a command line interface (CLI) for the AWS web services. Janelia Research Campus uses AWS S3 (Simple Storage Service) to
store all of the published MouseLight imagery, and you can easily use AWS CLI to search and download those files.

## Installation
First, you'll nned to install the AWS CLI on your computer. Follow Amazon's [instructions](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html).

## Configuration
Janelia Research Campus' buckets are set up to enable anonymous access, so no configuration is needed. If you already have an AWS account,
no changes to your configuration are needed.

## Listing files
Use the AWS CLI S3 *ls* command to list the contents of a bucket:
```
aws s3 ls s3://janelia-mouselight-imagery --no-sign-request
```
The *--no-sign-request* parameter is necessary for anonymous access. You may omit it if you're using your own AWS account.
You should see something similar to this:
```
                           PRE carveouts/
                           PRE images/
                           PRE neurons/
                           PRE registration/
                           PRE segmentation/
                           PRE tracings/
2022-05-12 13:53:15       4532 README.md
```
Theere is one object (file) in the listing above: README.md. The other entries are prefixes (indicated by __PRE__) - analogous to dieectories. If you want to see the objects and/or prefixes under a prefix, simply append it to the bucket:
```
aws s3 ls s3://janelia-mouselight-imagery/tracings/ --no-sign-request
```
...and you'll see a list of prefixes in the tracings prefix:
```
                           PRE Finished_Neurons/
                           PRE tracing_complete/
```
Note that any spaces in a prefix or object must be escaped with a backslash ("__\\__").
You can list files recursively with the *--recursive* parameter:
```
aws s3 ls s3://janelia-mouselight-imagery/tracings/tracing_complete/ --no-sign-request --recursive
2021-12-02 13:42:24      19968 tracings/tracing_complete/2014-06-24/G-001/Thumbs.db
2021-12-02 13:42:24    1079057 tracings/tracing_complete/2014-06-24/G-001/base.swc
2021-12-02 13:42:24    1333424 tracings/tracing_complete/2014-06-24/G-001/consensus.swc
2021-12-02 13:42:24      22567 tracings/tracing_complete/2014-06-24/G-001/dendrite.swc
2021-12-02 13:42:24         29 tracings/tracing_complete/2014-06-24/G-001/soma.txt
2021-12-02 13:42:24     232727 tracings/tracing_complete/2014-06-24/G-001/somaLoc.png
2021-12-02 13:42:24      95618 tracings/tracing_complete/2014-06-24/G-001/somaOnt.png
                        .
                        .
                        .
```
## Copying files
Use the AWS CLI S3 *cp* command to copy objects:
```
aws s3 cp s3://janelia-mouselight-imagery/tracings/tracing_complete . --recursive --no-sign-request
```
The above command will copy all onjects under janelia-mouselight-imagery/tracings/tracing_complete to your current directory. As the files
are copied, you'll see a running list of files and current status:
```
download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/soma.txt to 2014-06-24/G-001/soma.txt
download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/Thumbs.db to 2014-06-24/G-001/Thumbs.db
download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/dendrite.swc to 2014-06-24/G-001/dendrite.swc
download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/somaOnt.png to 2014-06-24/G-001/somaOnt.png
download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/uni2.swc to 2014-06-24/G-001/uni2.swc
download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-002/Thumbs.db to 2014-06-24/G-002/Thumbs.db
Completed 108.7 MiB/~9.5 GiB (9.1 MiB/s) with ~37 file(s) remaining (calculating...
```
It's always a good idea to simulate the copy first with the *--dryrun* parameter:
```
aws s3 cp s3://janelia-mouselight-imagery/tracings/tracing_complete . --recursive --no-sign-request --dryrun
```
You'll see what it would have copied:
```
(dryrun) download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/Thumbs.db to 2014-06-24/G-001/Thumbs.db
(dryrun) download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/base.swc to 2014-06-24/G-001/base.swc
(dryrun) download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/consensus.swc to 2014-06-24/G-001/consensus.swc
(dryrun) download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/dendrite.swc to 2014-06-24/G-001/dendrite.swc
(dryrun) download: s3://janelia-mouselight-imagery/tracings/tracing_complete/2014-06-24/G-001/soma.txt to 2014-06-24/G-001/soma.txt
                        .
                        .
                        .
```
