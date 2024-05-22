# Shop Signin Apps for Airtable Backend Using MIT IDs

This is a prototype signin app using the MIT ID Card API and Airtable backend.

See 'requirements.txt' for Python module requirements.  They can be installed via:
```
pip install -r requirements.txt
```

Both applications will need a secrets.py file as below:

```
#
# Credentials for Project Manus system
#
secrets = {
        'airtable_pat' : '<AIRTABLE PERSONAL ACCESS TOKEN>',
        'people_client_id' : '<MIT PEOPLE API CLIENT ID>',
        'people_client_secret' : '<MIT PEOPLE API CLIENT SECRET>,'
        'card_client_id' : '<MIT CARD API CLIENT ID>',
        'card_client_secret' : '<MIT CARD API CLIENT SECRET>'
}

#
# Shop Information
#
site = {
        'title' : '<SHOP TITLE TO DISPLAY IN APP>',
        'name' : '<SHOP NAME FROM AIRTABLE>',
        'description' : '<SHORT SHOP DESCRIPTION>',
        # Highlight colors for kiosk app
        'color-1' : '#57B99D',
        'color-2' : '#3D816E'
}

#
# A survey question.  Example is used in Project Manus makerspaces.
#
question = {
        'question' : 'What brings you to {} today?'.format(site['title']),
        'answers' : ['PERSONAL','RESEARCH','TRAINING','ENTREPRENEURSHIP','ON DUTY','CLUBS AND TEAMS','OTHER'],
        # leave 'freeform' blank to skip asking this question
        'freeform' : 'or enter class number'
}

#
# Full path to log file.  Null logs to stdio
#
logs = {
        'logfile' : ''
}

```
