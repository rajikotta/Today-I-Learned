## Gradle Dependencies for Testing In Android


- This is a brief guide to list out the gradle plugins and dependencies needed to perform testing of an android appplication.

- This document is focused mainly on the kotlin extension 




  - Junit : For basic testing. 

        `testImplementation "junit:junit:$junitVersion"`


  - Hamcrest : is a good tool for writing readable assertions much more like to a human sentence. 

        `testImplementation "org.hamcrest:hamcrest-all:$hamcrestVersion"`


  - Dependencies to add the core AndroidX Test core and ext dependencies.
  
        `testImplementation "androidx.test.ext:junit-ktx:$androidXTestExtKotlinRunnerVersion"`

        `testImplementation "androidx.test:core-ktx:$androidXTestCoreVersion"`

        `implementation "androidx.test:core:$androidXTestCoreVersion"`


  - Robolectric: is a  library that creates a simulated Android environment for tests and runs faster than booting up an emulator or running on a device.

        `testImplementation "org.robolectric:robolectric:$robolectricVersion"`


  - Architecture component core testing library.

        `testImplementation "androidx.arch.core:core-testing:$archTestingVersion"`


  - Dependency for stesting kotlin coroutines.

        `testImplementation "org.jetbrains.kotlinx:kotlinx-coroutines-test:$coroutinesVersion"`


  - for writing basic android instrumented tests.

        `androidTestImplementation "junit:junit:$junitVersion"`


  - AndroidX test library for creating fragments in tests and changing their state.

        `implementation "androidx.fragment:fragment-testing:$fragmentVersion"`


  - For performing integration tests

        `androidTestImplementation "androidx.test.espresso:espresso-core:$espressoVersion"`


  - Mockito : for creating mocks 

        `androidTestImplementation "org.mockito:mockito-core:$mockitoVersion"`


  - dexmaker-mockito : to use Mockito in an Android project

        `androidTestImplementation "com.linkedin.dexmaker:dexmaker-mockito:$dexMakerVersion"`


  - espresso-contrib : which contain testing code for more advanced views, such as DatePicker and RecyclerView


        `androidTestImplementation "androidx.test.espresso:espresso-contrib:$espressoVersion"`



   If the test rely on resources, need to enable *includeAndroidResources* in app gradle file



```android {
    // ...

    testOptions {
        unitTests {
            includeAndroidResources = true
       }
    }
  }

    ext {

    androidXTestCoreVersion = '1.2.0'

    androidXTestExtKotlinRunnerVersion = '1.1.1'

    archTestingVersion = '2.0.0'

    coroutinesVersion = '1.2.1'

    dexMakerVersion = '2.12.1'

    espressoVersion = '3.2.0-beta01'

    hamcrestVersion = '1.3'

    junitVersion = '4.12'

    mockitoVersion = '2.8.9'

    robolectricVersion = '4.3.1'
   
    }



