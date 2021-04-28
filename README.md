# stLFR-singularity

singularity image based on MGI stLFR docker image([https://github.com/MGI-tech-bioinformatics/stLFR_V1.3](https://github.com/MGI-tech-bioinformatics/stLFR_V1.3)).

## Introduction

As the MGI provides stLFR docker images. But it is difficult to run docker container on HPC clusters. [Singularity](https://sylabs.io/guides/3.7/user-guide/) provides a solution to run container on HPC. So I convert the stLFR docker image to singularity image.

## Defs

this folder contains the def file to build singularity image. You can use it to build your own singularity image with `singularity build -f <stLFR.sif> <stLFR.def>`。

Please do not override folders `/perl5, /stLFR` as they contain necessary files.

## Usage

When you successfully build a sif file(singularity image format), for example the `stlfr_v1.3.sif`, here is a simple example on how to use it.

```bash
db="/path_to_stlfr_db"
data="/path_to_data"
result="/path_to_result"
sif="stlfr_v1.3.sif"
name="test"

singularity exec \
    -B ${db}:/stLFR/db/ \
    -B ${data}:/data \
    -e \
    ${sif} \
    /bin/bash \
    /stLFR/bin/stLFR_SGE \
    ${result}/samples.list \
    ${result} >${name}.stLFR.log 2>&1
```

I just clean the env using `-e`  in case you set some wrong environment variables.

Please note this is just a shell command, and it may run for a long time.

## Data and Database

You can find all the things from MGI GitHub: [https://github.com/MGI-tech-bioinformatics/stLFR_V1.3](https://github.com/MGI-tech-bioinformatics/stLFR_V1.3).

## License

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions：

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.



