## WorkManager


This is a brief guide to start with WorkManager.

Android has enforced restriction on background work(such as Doze mode,App stand by and more restrictions on background service and broadcast receivers from API 26 onwards.) to ensure good app behaviour and maximise battery life.

 - WorkManager is a flexible api used to do background work even if the user navigates out of the app and we can add constraints under which the work should only trigger.
 - Part of Android Jetpack
 - Introduced in May 2018,Google I/O
 - Still in alpha stage(1.0.0-alpha09 on 19th Sep,2018)
 

Classes invovled in WorkManager API

 1. Worker
 2. WorkRequest
 3. OneTimeWorkRequest.Builder/PeriodicWorkRequest.Builder
 4. WorkManager
 5. WorkStatus
 6. WorkContinuation
 7. Data.Builder and Data
 

below are the steps to use work manager api

 

 1. Add dependency `android.arch.work:work-runtime:1.0.0-alpha09`.
 2.  Create a class by extending androidx.work.Worker,override doWork(),and add logic that should execute in background.doWork() returns Worker.Result which can be SUCCESS ,FAILURE or RETRY
 3. Get instance of WorkManager as  `WorkManager mWorkManager = WorkManager.getInstance();`
 4.  Now we have the work and workmanager ,next step is to create WorkRequest.  
 
 WorkRequest can be OneTimeWorkRequest or PeriodicWorkRequest.

	`mWorkManager.enqueue(OneTimeWorkRequest.from(BlurWorker.class));`
	
   or
   
	`   OneTimeWorkRequest.Builder blurBuilder =  
        new OneTimeWorkRequest.Builder(BlurWorker.class);    
 5. We can set input data to a work and set output data from a work

	   `Data.Builder builder = new Data.Builder();  
    builder.putString(KEY_IMAGE_URI, mImageUri.toString());  
    return builder.build();` 

     `blurBuilder.setInputData(createInputDataForUri());`
`blurBuilder.build();`


  6. We can make multiple workers execute in parallel or as a chain
 
	` 		WorkContinuation continuation = mWorkManager  
	  .beginUniqueWork(IMAGE_MANIPULATION_WORK_NAME,  
		 ExistingWorkPolicy.REPLACE,OneTimeWorkRequest.from(CleanupWorker.class));`


`continuation = continuation.then(blurBuilder.build());`

  
  The above code snippet is to create a unique work with the tag IMAGE_MANIPULATION_WORK_NAME  which will start with CleanupWorker then will do BlurWork
7. Add Constarints

    
    Constraints constraints = new Constraints.Builder()  
        .setRequiresCharging(true)  
        .build();  

`OneTimeWorkRequest save = new OneTimeWorkRequest.Builder(SaveImageToFileWorker.class)  
        .setConstraints(constraints)  
        .addTag(TAG_OUTPUT)  
        .build();  
continuation = continuation.then(save);`

 we can pass data through the chain of work as : set input data to first work by setting input data to WorkRequest ,then set output data inside doWork() of first work which can be retrieved in the next work ans do on.
 
 8. We can retrieve the work status in 3 ways
         

               

               1. getStatusById  returns LiveData<WorkStatus>
               2.getStatusesForUniqueWork returns status of works in a chain as LiveData<List<WorkStatus>>
               3.getStatusesByTag returns status of associated workrequest(associated through tag name) as LiveData<List<WorkStatus>>

WorkStatus also give output data 

    Data outputData = workStatus.getOutputData();



[Ref : Android Developer Docs](https://developer.android.com/topic/libraries/architecture/workmanager/)