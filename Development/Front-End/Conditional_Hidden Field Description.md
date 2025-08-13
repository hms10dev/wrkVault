Sarah shared this example (from WM Appointment screen) and document links with us for correcting the Forecast Policy History Used field description in view mode (it shows A, L, R, which is the seed data Id, instead of the description).  I just want to share this with you in case we have similar requirements like this in the future. 

Plain Text

"Dependencies": [  
           {  
             "Target": "attribute",  
             "Id": "AppointmentStatusDescription",  
             "Type": "view",  
             "Condition": "true",  
             "UID": "ListConfig1-Dependencies1"  
           },  
           {  
             "Target": "attribute",  
             "Id": "AppointmentStatusId",  
             "Type": "edit",  
             "Condition": "true",  
             "UID": "ListConfig1-Dependencies2"  
           },

Reference file: [https://bitbucket.org/manhattanassociates/ui-metadata/src/f17c3c5eb6a98d638db63754a3d80bdb1ea27a60/metadata/com-manh-cp-appointment/pages/Appointment/AppointmentDetails.json#lines-501,504,511](https://bitbucket.org/manhattanassociates/ui-metadata/src/f17c3c5eb6a98d638db63754a3d80bdb1ea27a60/metadata/com-manh-cp-appointment/pages/Appointment/AppointmentDetails.json#lines-501,504,511 "https://bitbucket.org/manhattanassociates/ui-metadata/src/f17c3c5eb6a98d638db63754a3d80bdb1ea27a60/metadata/com-manh-cp-appointment/pages/Appointment/AppointmentDetails.json#lines-501,504,511")

Conf doc: [https://manhattanassociates.atlassian.net/wiki/spaces/CF/pages/940117941/Dependencies](https://manhattanassociates.atlassian.net/wiki/spaces/CF/pages/940117941/Dependencies "https://manhattanassociates.atlassian.net/wiki/spaces/CF/pages/940117941/Dependencies")

Thanks,

Milly