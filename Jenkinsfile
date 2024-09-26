#!groovy
// This ensures that the libraries are downloaded and made accessible during runtime.
@Library('roboshop-shared-library')_ // This annotation tells Jenkins to load the shared library named roboshop-share-library.

// here created some parameters as a map 
def configMap= [                  // configMap is a Groovy Map that holds key-value pairs.
    application: "nodeJSVM",
    component: "catalogue"
]

// passing parmeters to the pipeline and this is a .groovy file name and function inside it
pipelineDecission.decidepipeline(configMap)