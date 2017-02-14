# SFDC-FEA
Programming pattern for salesforce.com's apex triggers.

This is nothing more than what I have found is one of the best ways to improve efficiency in processing records within salesforce.com's apex triggers. 

### How I did it before FEA

Most of the time when I personally created triggers and tried to organized everything in it without thinking on any trigger framework.. depending on the functionality needed... Let's say I need to do some validation on records and also I want to update some fields based on other field values, I would probably do a trigger and attach it to a before event, like the following:

```java
trigger MyTrigger on Referral__c (before update) {
    
        HelperZ.ValidateRecords(Trigger.new, Trigger.OldMap);
        
        HelperZ.ChangeFieldsAutomatically(Trigger.New, Trigger.OldMap);
        
        HelperZ.AutoCheckForProcessZ(Trigger.New, Trigger.OldMap);
          
}
```

The previous code is perfectly fine, each of the helper's method will internally iterate the Trigger.new list and they will identify any data specific criteria and maybe do whatever they need to do...  the following is some example on how any of those methods would look like:


```java
public class HelperZ {
        public static void ValidateRecords(List<MyObject__c> newList, Map<Id, MyObject__c> oldMap){
          
           for(MyObject__c myObj : newList){
             if(myObj.fieldA__c != oldMap.get(myObj.Id).fieldA__c && oldMap.get(myObj.id).fieldA__c != null)
             {
               myObj.fieldA__c.addError('No changes allowed to this field after it has been populated');
             }
           }
           
          
        }
        
       
       public static void ChangeFieldsAutomatically(List<MyObject__c> newList, Map<Id, MyObject__c> oldMap){
           for(MyObject__c myObj : newList){
             if(myObj.fieldA__c != oldMap.get(myObj.Id).fieldA__c && myObj.fieldA__c == 'x1' )
             {
               myObj.fieldB__c = 'z1';
             }
             
              if(myObj.fieldA__c != oldMap.get(myObj.Id).fieldA__c && myObj.fieldA__c == 'x2' )
             {
               myObj.fieldB__c = 'z2';
             }
             
              if(myObj.fieldA__c != oldMap.get(myObj.Id).fieldA__c && myObj.fieldA__c == 'x3' )
             {
               myObj.fieldB__c = 'z3';
             }
             
             
           }
       }
       
       
       public static void AutoCheckForProcessZ(List<MyObject__c> newList, Map<Id, MyObject__c> oldMap){
       
          for(MyObject__c myObj : newList){
             if(myObj.fieldA__c != oldMap.get(myObj.Id).fieldA__c && myObj.fieldA__c == 'x0' )
             {
               myObj.fieldToCheck__c = true;
             }
             
           }
       
       
       }
       
   
}
```


### Pending
* Include additional content.

