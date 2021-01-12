# Envisioned Voice Assistant Dialogues

This data set was collected as part of a research project at LMU Munich (Germany), University of Bayreuth (Germany), and the University College Dublin (Ireland). This research project will be published in the proceedings of the ACM CHI Conference on Human Factors in Computing Systems in 2021 (CHI '21). You may find the project website here: http://www.medien.ifi.lmu.de/envisioned-va-dialogues/

The dataset consists of 1,854 written dialogues between a user and a voice assistant, which were envisioned by 205 people in an online survey. In particular, we asked participants to envision and write down dialogues with a *perfect* voice assistant without any technical limitations for nine scenarios (cf. below). In the survey instructions, we highlighted that the conversation could be initiated by both parties, and also provided an example scenario with two example dialogues (one initiated by the user, the other by the voice assistant). Participants were then presented with the eight different scenarios in random order before concluding with an open scenario, where they were given the opportunity to think of another situation where they would like to use the perfect voice assistant. For each scenario, participants were asked to first select who is speaking from a dropdown menu ("You" or "Voice assistant") and then write down what the selected speaker is saying).

## Scenarios
We prompted participants with eight scenarios. These scenarios were based on the most popular use cases for Google Home and Amazon Alexa / Echo as recently identified by <a href="https://dl.acm.org/doi/abs/10.1145/3311956">Ammari et al. (2019)</a> from 250,00 command logs of users interacting with smart speakers. In addition, we included an open scenario where participants could describe a situation in which they would like to use a voice assistant. Each scenario contained a descriptive part and a specific issue which participants should address and solve in their envisioned dialogue between a user and a perfect voice assistant.

These are the scenarios:
<table>
  <tr>
    <th>Name</th>
    <th>Description & Issue</th>
  </tr>
  <tr>
    <td>Search</td>
    <td>You want to go to the cinema to see a film, but you do not know the film times for your local cinema.</td>
  </tr>
  <tr>
    <td>Music</td>
    <td>You are cooking dinner. You are on your own and you like to listen to some music while cooking.</td>
  </tr>
  <tr>
    <td>Internet of Things</td>
    <td>You are going to bed. You like to read a book before going to sleep. You often fall asleep with the lights on.</td>
  </tr>
  <tr>
    <td>Volume</td>
    <td>You are listening to loud music, but your neighbours are sensitive to noise.</td>
  </tr>
  <tr>
    <td>Weather</td>
    <td>You are planning a trip to Italy in two days but do not know what kind of clothing to pack. You like to be prepared for the weather. </td>
  </tr>
  <tr>
    <td>Joke</td>
    <td>You and your friends are hanging out. You like to entertain your friends, but the group seems to have run out of funny stories.</td>
  </tr>
  <tr>
    <td>Conversational</td>
    <td>You are going to bed, but you are having trouble falling asleep.</td>
  </tr>
  <tr>
    <td>Alarm</td>
    <td>You are going to bed. You have an important meeting early next morning, and you tend to oversleep.</td>
  </tr>
  <tr>
    <td>Open Scenario</td>
    <td>Participants were asked to think about another situation in which they would like to use the perfect voice assistant.</td>
  </tr>
</table>

## Questionnaires
In addition to writing down dialogues between a user and a voice assistant, we also asked participants about their experience with existing voice assistants and for demographic infromation. Furthermore, participants filled out the 60 items Big Five Inventory-2 personality questionnaire by <a href="https://psycnet.apa.org/record/2016-17156-001">Soto and John (2017)</a>. 

## Participants


## Reference
A full description of the data, methodology and analyses as well as sample conversations and user instructions can be found in our EMNLP paper cited below. (Please cite in your work where relevant.)

@inproceedings{byrne-etal-2019-taskmaster, title = {Taskmaster-1:Toward a Realistic and Diverse Dialog Dataset}, author = {Bill Byrne and Karthik Krishnamoorthi and Chinnadhurai Sankar and Arvind Neelakantan and Daniel Duckworth and Semih Yavuz and Ben Goodrich and Amit Dubey and Kyu-Young Kim and Andy Cedilnik}, booktitle = {2019 Conference on Empirical Methods in Natural Language Processing and 9th International Joint Conference on Natural Language Processing}, address = {Hong Kong}, year = {2019} }

EXPLANATION OF DATA FILES

The bulk of the corpus is provided in JSON format in two data files. self-dialogs.json contains all the one-person dialogs. woz-dialogs.json contains all the WOz dialogs.

One-person dialogs can be divided into train/dev/test sets by matching the dialog IDs from the following files:

train.csv
dev.csv
test.csv
Additionally, the following files are provided to describe the data structure and annotation schema.

sample.json - A sample conversation describing the format of the data.
ontology.json - Schema file describing the annotation ontology.
Each conversation in the data file has the following structure:

conversationId: A universally unique identifier with the prefix 'dlg-'. The ID has no meaning.
utterances: An array of utterances that make up the conversation.
instructionId: A reference to the file(s) containing the user (and, if applicable, agent) instructions for this conversation.
Each utterance has the following fields:

index: A 0-based index indicating the order of the utterances in the conversation.
speaker: Either USER or ASSISTANT, indicating which role generated this utterance.
text: The raw text of the utterance. In case of self dialogs, this is written by the crowdsourced worker. In case of the WOz dialogs, 'ASSISTANT' turns are written and 'USER' turns are transcribed from the spoken recordings of crowdsourced workers.
segments: An array of various text spans with semantic annotations.
Each segment has the following fields:

startIndex: The position of the start of the annotation in the utterance text.
endIndex: The position of the end of the annotation in the utterance text.
text: The raw text that has been annotated.
annotations: An array of annotation details for this segment.
Each annotation has a single field:

name: The annotation name.
EXPLANATION OF ONTOLOGY

Dialog annotations are based on the API calls associated with each type of task-based dialog. The full JSON description of the ontology can be found in ontology.json. Each conversation was annotated by two workers. Both annotations are included in this collection.

The API-based annotations can be divided into two categories:

API argument labels: These refer to the parameter values specified for a given transaction. For example, a pizza order must minimally provide values for store name, number of pizzas, sizes, topping(s) and sometimes crust type (known as 'required' parameters in ontology.json). Named pizzas like 'veggie lovers' come with a predetermined set of toppings and so only the number pizzas and sizes are required. Users may also specify optional arguments (known as 'optional' parameters in ontology.json) such as 'extra cheese' or substitutions like 'pesto instead of tomato sauce', omissions like 'no tomatoes', etc.
Transaction status labels: In addition to the parameter values, the success or failure of the transaction itself is labeled with 'accept' or 'reject'. If the dialog only makes general reference to a transaction, e.g. 'OK your pizza has been ordered' or 'Sorry we just discontinued that pizza so it's no longer available', the label 'accept' or 'reject' is added to the vertical name, i.e. 'pizza_ordering.accept'. However, in most cases these labels are added to the individual parameters involved in the transaction, whether accepted or rejected. For example, in 'It looks like we are out of pepperoni tonight', 'pepperoni' would be labeled 'type.topping.reject' while the rest of the values would get the 'accept' label.
Please note: 146 dialogs were left unannotated due to the fact that their content has to do more with preference discussion than task completion. We will update the corpus with these dialgos flagged as such.

API VALIDATION

The ontology classifies API arguments for each vertical into 'required' and 'optional'. For example. 'name.restaurant' is a required parameter whereas 'type.seating' is optional during a restaurant reservation. Conversations that did not contain any of the 'required' parameters were removed from the released dataset.

Additionally, no requirement was imposed on the minimum number of 'required' parameters to be eligible for being part of the released dataset. A common theme among conversations with missing 'required' parameters was the worker's assumption that they were talking to the business directly. For example, in pizza ordering dialogs workers sometimes failed to give a business name. Similar mistakes are seen with the origin or destination fields for ride booking, shop name for auto repair, number of guests of table reservations, etc.

TRANSCRIPTION NOTES

In a separate task, transcription of crowdsourced user utterances from the two-person dialogs were checked for errors but may still include an occasional typo, misspelling or ungrammatical sequence. In cases where a dialog failed to make sense, workers doing these corrections were given the freedom to insert or delete turns or replace entire phrases with language that made the dialog follow a more sensible path. Shorthand typing conventions originally used by the call center operators such as 'cuz', 'lol' and other non-standard English phrases were left as is. Disfluencies such as 'they um, they want Korean cuisine' were also usually transcribed as spoken, but sometimes transcribers corrected them.

In case you have any comments or questions, please contact sarah.voelkel@ifi.lmu.de
