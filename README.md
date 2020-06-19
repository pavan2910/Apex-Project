<apex:page sidebar=”false” controller=”CloneTestingRecordClass”>
<apex:form >
<apex:pageBlock >
<apex:pageBlockSection >
<apex:pageBlockTable value=”{!records}” var=”r”>
<apex:column headerValue=”Name”>
{!r.Name}
</apex:column>
<apex:column headerValue=”City”>
{!r.City__c}
</apex:column>
<apex:column headerValue=”Country”>
{!r.Country__c}
</apex:column>
<apex:column headerValue=”Phone”>
{!r.phone__c}
</apex:column>
<apex:column headerValue=”Action”>
<apex:commandLink value=”Clone” action=”{!clonedRec}”>
<apex:param name=”rId” value=”{!r.Id}” assignTo=”{!rId}”/>
</apex:commandLink>
</apex:column>
</apex:pageBlockTable>
</apex:pageBlockSection>
</apex:pageBlock>
</apex:form>
</apex:page>

Apex class:
public with sharing class CloneTestingRecordClass {
public PageReference clonedRec() {
DataLoadTest__c selectedRecord = [select Id,name,city__c,country__c,phone__c from DataLoadTest__c where id=:rId];
dataLoadtest__c lstnew = selectedRecord.clone(false);
insert lstnew;
pagereference ref = new pagereference(‘/apex/cloneRecordTesting’);
ref.setredirect(true);
return ref;
}
public String rId{get;set;}
List<DataLoadTest__c> lstdlt = new List<DataLoadTest__c>();
public List<DataLoadTest__c> getRecords() {
lstdlt = [select Id,name,city__c,country__c,phone__c from DataloadTest__c];
return lstdlt;
}
}
