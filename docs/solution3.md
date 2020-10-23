```nextflow
workflow flow1 {
    take: sequences
    main:
    splitSequences(sequences) | reverseSequence | view()
}
```
