# Extra content for <a href="../../objectives/O11_Customer_Complaint_Analysis/">Objective 11) Customer Complaint Analysis</a>

## All the complaints

The pcap file for the objective contains 16 submissions to the customer complaint system.  

If we use the Wireshark filter `http.request.method == POST` then we will get all 16 submissions and can read through each of them in the same way that we did to complete the main objective.

Another method would be to use the `tshark` command line utility to output just the form data for each POST packet.<br>
`tshark -r jackfrosttower-network.pcap -Y "http.request.method == "POST"" -T fields -e urlencoded-form.value`

All complaint submissions are listed in the table below.

| Name | Troll ID | Guest Info | Description |
| ---- | -------- | ---------- | ----------- |
Klug|2234|Funny looking man in room 1145|I carry suitcase to room. Throw bag at bed and miss a little. Man is angry. He say suitcase is scuff. I say his face is scuff. He is more angry and I get no tip.|
Gavk|2354|Annoying woman in room 1239|Woman call desk and complain that room is cold. I go to room, knock on door, and tell her nice that I eat beans at lunch and can warm room up. She slam door in Gavk face. So mean.|
Bluk|2367|Boring humans in room 1128|I bring room service order. Use key card to go in. Woman getting undress. She scream and throw shoe at me. Shoe is tasty, but it not make up for her hurt my ears with scream.|
Euuk|1973|Ugly, mean couple in room 1032|Euuk do an innocent "crop dust" in elevator as it reach ground floor. No biggie - everyone do this sometimes. Couple get in. Begin to retch. Look at me with mean-type nastiness. I have bad feels.|
Crag|2351|Bald man in room 1212|Crag get in elevator. Man get in too. Crag push ALL buttons. Crag giggle because is funny joke. Man is no thinking funny. He has bad humor. He call Crag "unthinking brute." Crag is not brute.|
Urgh|2633|Stupid man in room 1215|Bring drink to man at slot machine. Spill it on him a little. Urgh go to lick it off of him and he is angry. Say his is "shock" at Urgh behavior and lick is a bad idea. He is silly and mean.|
Yaqh|2796|Snooty lady in room 1024|Lady call desk and ask for more towel. Yaqh take to room. Yaqh ask if she want more towel because she is like to steal. She say Yaqh is insult. Yaqh is not insult. Yaqh is Yaqh.|
Flud|2083|Very cranky lady in room 1024|Lady call front desk. Complain "employee" is rude. Say she is insult and want to speak to manager. Send Flud to room. Lady say troll call her towels thief. I say stop steal towels if is bother her.|
Hagg|2013|Incredibly angry lady in room 1024|Lady call front desk. I am walk by so I pick up phone. She is ANGRY and shout at me. Say she has never been so insult. I say she probably has but just didn't hear it.|
Muffy VonDuchess Sebastian|I don't know. There were several of them.|Room 1024|I have never, in my life, been in a facility with such a horrible staff. They are rude and insulting. What kind of place is this? You can be sure that I (or my lawyer) will be speaking directly with Mr. Frost!|
Quib|2539|Ugly little man in room 1121|He call desk and say his shoes need shine. He leave outside door. I go and get. I spit shine. One spot on shoes is bad so I lick a little. Quite tasty. I accidental eat shoe. I take other shoe back. I am proud I no eat. He is mean at me.|
Bloz|2323|Nasty bad woman in room 1125|Bloz have tacos for lunch. Later, Bloz have very bad tummy and need to use potty immediate. Use key card on room on 11 floor. Bloz in bathroom doing business. Lady come in and scream. Bloz business quick done. She is rude.|
Wuuk|2987|Very crabby woman in room 1125|Lady call desk and say toilet plug. Wuuk take plunger and go to room. Wuuk make innocent comment that lady poop like troll and say Wuuk is "outrageous."<br>Does that mean handsome?|
Kraq|2383|Rude couple in room 1117|Kraq make teensy comment about man having bad toupee. Turn out it is not toupee. Kraq stand by comment - man have hair look like bad toupee. Man is angry and call Kraq many bad word. Kraq is just a pawn in great game of life.|
Ikky|2743|Family in room 1226|Lady is sit in lobby holding wonderfully ugly doll. Ikky like ugly doll and ask where she get. Ikky use to decorate for Halloween. She get angry because is her baby. She say "I never!" Ikky say she must have at least once.|
Stuv|2833|Grumpy man in room 1119|Man call front desk to complain about room be stuffy. Stuv say he is happy to get man and throw outside. Lot's of fresh air. And polar bears.|

