# QNAMaker Deployments

The purpose of this document is to provide an idea on how to perform automated deployments of some of the server side resources like QnAMaker. 

This is primarily created and maintained by developers or various researches/data experts of departments across org to maintain a workable, acceptable and highly flexible question/answer set.

Since this is a resource not primarily managhed by devs, we need a way to automate deployment of the same. Similar procedure can be followed for other such as Logic App, Bots etc.

## Assumptions

- QnAMaker is created already through Portal or by some other means
- KnowledgeBases - known as KBs may or may not exist
- Automated Deployment scripts will add/update KBs

## Folders

### Deployments -

- QnAMakerDeploy - This folder contains actual deplouyment scripts for Create/Update QnAMaker KBs. Exact same structure will be checked into the repository. Tools like Azure DevOps can then run scripts to send data to QnAMaker resource using REST API endpoints

  1. Create - Script(s) in this folder would allow users to Create a new KB. The script follows JSON file approach, where one has to specify the Questions/Answers as json fields

     ```
     {
       "id": 0,
       "answer": "Let us go to INOX!!",
       "source": "General",
       "questions": [
       	"Where to go for a movie?"
       ],
       "metadata": []
     }
     ```

     

  2. CreateByKeyValue - Primarily for people from non-dev background, can actually update a very simple key value JSON. 

     ```
     {
         "name": "CreateKB by KeyValue",
         "qnaList": [
             
             { "How is it today": "Nice and Sunny" },
             { "How are you": "Fit & Healthy" },
             { "Like this model": "I love Mercs, Audis" }
     
         ]
     }
     ```

  3. CreateByURL - Similar approach but using URLs - i.e. KB files stored in some accessible locations as per QnAMaker prescribed standard

     ```
     {
         "name": "From XLX File FAQ",
         "urls": [
     
             "https://docs.microsoft.com/en-us/azure/cognitive-services/Emotion/FAQ"
         ]
     
     }
     ```

  4. Update - Scripts here would allow users to add/update/delete questions from a particular KB

     ```
     {
         "update": {
             "qnaList": [
                 {
                     "id": 1,
                     "answer": "Let us explore the new PVR at Kolkata!",
                     "source": "General",
                     "questions": {
     
                         "add": [ "How to go there223?" ]
                         
     
                      }
                 }
             ]
         }
     }
     ```

     

  5. UpdateByURL

     ```
     {
         "update": {
             "urls": [
     
                 "https://docs.microsoft.com/en-in/azure/cognitive-services/qnamaker/faqs",
                 "https://docs.microsoft.com/en-us/bot-framework/resources-bot-framework-faq"
             ]
         }
     }
     ```

     

  6. Train

     ```
     {
         "feedbackRecords": [
             {
                 "qnaId": 1,
                 "userId": "de3bf09894a645da88a10b873de13c19",
                 "userQuestion": "qna maker with luis223"
             }
         ]
     }
     ```