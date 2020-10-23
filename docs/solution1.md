```nextflow
#!/usr/bin/env nextflow

nextflow.enable.dsl=2

/*
* Let's create the channel `my_files`
* using the method fromPath 
*/

Channel
    .fromFilePairs( "file_{1,2}.txt" )
    .set {my_fyles}

my_fyles.view()
```
