 # 🌱 QuickNote: Item Location Component

####  ⌚️ Date: Aug 2, 2022

---
### 📝  Notes
```Java
<entity name="lpnCriteria" type="config" securityScope="profile" profilePurpose="system"  
>  
    <property name="criteriaId" type="id" description="criteria ID"/>  
    <property name="scanLpn" type="booleanTrue"/>  
    <property name="promptExpireDate" type="date"/>  
    <property name="displayUom" type="quantity"/>  
  
</entity>
```



profilePurpose="itl::uomConfig"


```Java
<relationship fromEntity="Lpn"  toEntity="LpnDetails" cardinality="many"  
              accessDirection="forward" businessKeyJoin="true"/>
```

fromProperty="batchNbr"


### Application/Todo:
- [ ] [[#Stories for ItemLocation Code Coverage Increase]]


## Stories for ItemLocation Code Coverage Increase



### Jira link:
- https://manhattanassociates.atlassian.net/browse/AI-2249

### Exisiting code coverage can be accessed here:
- [https://sonarcloud.io/component_measures?metric=new_lines_to_cover&view=list&id=com-manh-cp-itemlocation](https://sonarcloud.io/component_measures?metric=new_lines_to_cover&view=list&id=com-manh-cp-itemlocation "https://sonarcloud.io/component_measures?metric=new_lines_to_cover&view=list&id=com-manh-cp-itemlocation")

### The entities I am working on :
- ModelStore and Related Classes

### Related Classes that need increased Code Coverage:

^77efe0

- ModelStoreSetupController
- ModelStoreSetupServiceImpl
- ModelStoreSetupMapServiceImpl

### Branch Naming Convention:

- pullrequest/==**JIRA_Ticket_Number_Assigned_To_Me**==
- pullrequest/AI-2249
- 
