# Work Manager
### What is a Work Manager :
WorkManager is a library used to enqueue deferrable work that is guaranteed to execute sometime after its Constraints are met. WorkManager allows observation of work status and the ability to create complex chains of work.

### Why is a Work Manager :
* To optimise the battery consumption.
* To maintain the background work correctly without affecting the processing speed
* Deferrable and Guaranteed background work.
* To get rid of the boilerplate code. 
* Backwards Compatible up to API 14
  * Uses JobScheduler on devices with API 23+
  * Uses a combination of BroadcastReceiver + AlarmManager on devices with API 14 - 22

### Components of Work Manager :
