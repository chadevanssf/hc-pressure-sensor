# hc-pressure-sensor

Health Cloud Pressure Sensor package, simulating IOT type devices

## Install

```sh
sfdx force:user:permset:assign -n PressureSensor
sfdx force:data:tree:import -p ./data/Account-Asset-plan.json
sfdx force:data:tree:import -p ./data/Contact-Patient_State__c-plan.json
```

## Dev

```sh
sfdx force:data:tree:export -p -q ./data/account-asset.soql -d ./data/
sfdx force:data:tree:export -p -q ./data/contact-patient_state.soql -d ./data/
```

## Test

```sh
List<SObject> events = new List<SObject>();

// Patient Motion
Patient_Motion__e pmEvent = new Patient_Motion__e();
pmEvent.PatientID__c = 'MRN-123456';
pmEvent.Orientation__c = 'ACTIVE';
//pmEvent.Orientation__c = 'SITTING';
//pmEvent.Orientation__c = 'LAYING';
pmEvent.LastMotion__c = 90;

events.add(pmEvent);
        
//List<Database.SaveResult> results = EventBus.publish(events);

//List<SObject> events = new List<SObject>();

// Patient Pressure
Patient_Pressure__e ppEvent = new Patient_Pressure__e();
ppEvent.PatientId__c = 'MRN-123456';
ppEvent.Message__c = '{"laying":"hide","escalate":"hide","adjusted":"hide"}';
//ppEvent.Message__c = '{"laying":"show","escalate":"hide","adjusted":"hide"}';
//ppEvent.Message__c = '{"laying":"hide","escalate":"show","adjusted":"hide"}';
//ppEvent.Message__c = '{"laying":"hide","escalate":"hide","adjusted":"show"}';

events.add(ppEvent);
        
List<Database.SaveResult> results = EventBus.publish(events);
```