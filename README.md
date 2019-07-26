# hc-pressure-sensor

Health Cloud Pressure Sensor package

## Install

sfdx force:user:permset:assign -n PressureSensor
sfdx force:data:tree:import -p ./data/Account-Asset-plan.json
sfdx force:data:tree:import -p ./data/Contact-Patient_State__c-plan.json

## Dev

sfdx force:data:tree:export -p -q ./data/account-asset.soql -d ./data/
sfdx force:data:tree:export -p -q ./data/contact-patient_state.soql -d ./data/


## Test

Patient_Motion__e  newEvent = new Patient_Motion__e();
newEvent.PatientID__c = 'MRN-123456';
//newEvent.Orientation__c = 'LAYING';
newEvent.Orientation__c = 'ACTIVE';
newEvent.LastMotion__c = 90;

List<SObject> events = new List<SObject>();
events.add(newEvent);
        
List<Database.SaveResult> results = EventBus.publish(events);