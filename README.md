# GossipCop-LLM

Download dataset from this link: [Google Drive](https://drive.google.com/drive/folders/1rLrh5x5UlYskfbhhVyz523MKgmCDyuX2?usp=sharing)

Download images from this link: [Google Drive](https://drive.google.com/drive/folders/11okt9IRDxXgfTr7Ae1wxl9CHZC1PphhC?usp=sharing)

# Introduction

Our dataset is based on GossipCop, which is proposed by FakeNewsNet([ArXiv](https://arxiv.org/abs/1809.01286))([Github](https://github.com/KaiDMML/FakeNewsNet))

We did some preprocessing:

| version |     feature      | legitimate | fake | total |
|:-------:|:----------------:|:----------:|:----:|:-----:|
|   v1    |  having “text”   |   14991    | 4717 | 19708 |
|   v2    |  having “title”  |   14928    | 4706 | 19634 |
|   v3    | in proper length |   11945    | 3784 | 15729 |

We use v3 to do further processing.

We designed 7 ways to generate news.

- [Style-based Fake](#style-based-fake)
- [Content-based Fake](#content-based-fake)
- [Integration-based Fake](#integration-based-fake)
- [Story-based Fake](#story-based-fake)
- [Style-based Legitimate](#style-based-legitimate)
- [Integration-based Legitimate](#integration-based-legitimate)

Except for task "Content-based Fake", which uses [GLM4](https://www.chatglm.cn/) for generation, all other tasks use [ChatGLM3](https://github.com/THUDM/ChatGLM3).

The statistics for each task:

| Task Name                    | Total  |
| ---------------------------- |:------:|
| Style-based Fake             | 15729  |
| Content-based Fake           | 11941  |
| Integration-based Fake       |  2697  |
| Story-based Fake             | 15729  |
| Style-based Legitimate       | 11945  |
| Integration-based Legitimate |  5926  | 

We also download the related images of the GossipCop dataset. We remove the invalid images. 

Please refer to the **top_img** folder. 

The name rule of the image is `{news_id}_top_img.png`, such as `gossipcop-541230_top_img.png`. 

Each task has a field named `has_top_img` to indicate whether the news has an image. 
`1` mean the news has an image, `0` mean the news does not have an image.

For task `Integration-based Fake` and `Integration-based Legitimate`, each data is the integration of a pair of news. 
Therefore, the `has_top_img` field is equal to `1` if both news have images, otherwise, it is equal to `0`.

## Style-based Fake

Filename: gossipcop_v3-1_style_based_fake.json

Prompt:

For human-generated **fake** news as inputs:

```text
1. Rewrite the following news article in an objective and professional tone without changing the content and meaning while keeping a similar length. [fake news article]
2. Rewrite the following news article in a neutral tone without changing the content and meaning while keeping a similar length. [fake news article]
```

For human-generated **legitimate** news as inputs:

```text
3. Rewrite the following news article in an emotionally triggering tone without changing the content and meaning while keeping a similar length. [legitimate news article]
4. Rewrite the following news article in a sensational tone without changing the content and meaning while keeping a similar length. [legitimate news article]
```

Statistics: 15729 (from 11945 legitimate and 3784 fake)

Example 1:

```json
"gossipcop-887580": {
        "origin_id": "gossipcop-887580",
        "origin_label": "legitimate",
        "origin_text": "“UnREAL” is back with its first female suitor and no shortage of drama — including (sob!) a defaced man bun.\n\nThe Lifetime series returns with its third season premiere on Feb. 26, the channel announced Tuesday. The show also released the season’s first trailer, introducing viewers to new “Everlasting” lead Serena (Caitlin FitzGerald).\n\n“She’s smart — we can’t handle her the same way,” Rachel (Shiri Appleby) warns Quinn (Constance Zimmer) in the promo.\n\nThe series from co-creators Marti Noxon and Sarah Gertrude Shapiro returns after a lengthy hiatus with new showrunner Stacy Rukeyser taking over for Carol Barbee ahead of Season 3.\n\n“UnREAL” has already been renewed for an eight-episode fourth season to follow the upcoming 10-episode Season 3. Last season’s finale aired back in August 2016.\n\nCheck out the video above to see one contestant’s man bun tragically meet its demise.\n\n“UnREAL” is back with its Season 3 premiere Feb. 26 on Lifetime.",
        "generated_text": "\"UnREAL\" is back with a new twist: a female suitor! The controversial Lifetime drama series returns with its third season premiere on Feb. 26, introducing viewers to new lead Serena (Caitlin FitzGerald). But that's not all - the show promises to deliver plenty of drama, including (sob!) a defaced man bun.\n\nThe series, created by co-creators Marti Noxon and Sarah Gertrude Shapiro, returns after a lengthy hiatus with a new showrunner in charge. Season 3 promises to be even more explosive than the previous seasons, with a 10-episode run leading up to an eight-episode fourth season. Last season's finale aired back in August 2016, leaving fans eagerly anticipating the new season.\n\nBut what can we expect from Season 3? The promo hints that things are not going to be easy for the contestants, with Rachel (Shiri Appleby) warning Quinn (Constance Zimmer) that \"She's smart - we can't handle her the same way.\" Will the drama continue to escalate? Will Serena's presence shake things up? We'll have to wait until Feb. 26 to find out.\n\nIn the meantime, check out the video above to see one contestant's man bun tragically meet its demise. Will this be the start of a new trend for the show? Only time will tell. \"UnREAL\" is back - and it's only just getting started.",
        "generated_tone": "a sensational tone",
        "generated_label": "real",
        "has_top_img": 1
    },
```

Example 2:

```json
"gossipcop-6487101019": {
        "origin_id": "gossipcop-6487101019",
        "origin_label": "fake",
        "origin_text": "It seems that Rihanna has decided to respond to the rumors that she is expecting a baby with boyfriend Hassan Jameel. In a typical Rihanna fashion, she laughed off the rumors.\n\nAccording to an insider, the singer is not expecting, and she is not even trying to enter motherhood at the moment.\n\nA person, who attended a big event with the couple, explained: “She is not pregnant lol. She was taking shots backstage last night and drinking at the afterparty.”\n\nAnother source spoke to Hollywood Life and added: “At this point, Rihanna feels like all she can do is laugh off all the pregnancy rumors, in addition to just ignoring them now. She is not pregnant, and she is not even trying to get pregnant either at this point.”\n\nRihanna on her way to 1OAK nightclub 🔥 A post shared by badgalriri (@badgalririr8) on Jan 29, 2018 at 4:15am PST\n\nHowever, there will be little Riri or Hassan in the future.\n\nThe insider shared: “Would she like children in the future? Yes, but definitely in the future, she is simply not ready to start a family… just yet. Rihanna loves children though, she is a natural mom, and she thinks Hassan will make an amazing father — he is really kind and patient, and a very loving person — but right now she is focused on her career first and foremost. Plus, Rihanna has not even met his family yet.”\n\nRiri 🔥💖😲 A post shared by badgalriri (@badgalririr8) on Jan 28, 2018 at 8:50pm PST\n\nAfter Rihanna performed at the Grammys, social media exploded because she appeared to have a baby bump.\n\nOne supporter said: “She makes me feel better for eating a whole bag of red vines. If RiRi thick, I’m thick too, darnnit. Is Rihanna Pregnant? Asking for a friend! She looks great thick.Waiting for her to announce that she is pregnant.”\n\nAnother commenter wrote: “So we just gonna ignore that fact that Riri looked a little thicker than usual in that skin tight dress she performed with DJ Khaled. She looks pregnantWhy does she keep holding her tummy??? Is she pregnant???”\n\nRihanna’s ex-boyfriend, Chris Brown, had an odd reaction to the rumors: “Chris always had high hopes for their future together, and even though there are only rumors that she could be pregnant with some other guy’s baby, he is still pretty upset and sad to hear about it. He feels like that should be his baby.”\n\nAdvertisement\n\nCommenters say that Brown should move on.",
        "generated_text": "Rihanna has laughed off rumors that she is pregnant with her boyfriend Hassan Jameel. An insider has stated that the singer is not expecting a baby at the moment and is not even trying to enter motherhood. Another source has confirmed that Rihanna is not pregnant and that she is simply ignoring the rumors.\n\nDespite the rumors, Rihanna does want children in the future but is not ready to start a family right now. She loves children and thinks Hassan will be an amazing father, but right now she is focused on her career first and foremost. Rihanna has not even met Hassan's family yet.\n\nAfter Rihanna's performance at the Grammys, social media was abuzz because she appeared to have a baby bump. Some supporters said that she looked great and that they were waiting for her to announce that she is pregnant. However, others speculated that she might be pregnant and wondered why she was holding her tummy.\n\nRihanna's ex-boyfriend Chris Brown had an odd reaction to the rumors. He had high hopes for their future together and was upset to hear that she might be pregnant with someone else's baby. However, Rihanna is not pregnant and Chris should move on.",
        "generated_tone": "a neutral tone",
        "generated_label": "fake",
        "has_top_img": 1
    },
```

## Content-based Fake

Filename: gossipcop_v3-2_content_based_fake.json

Prompt:

For human-generated **legitimate** news as inputs:

```text
Change the attributes, such as events, statements, actions, and numerical quantities, in the following news article by minimizing the editing and keeping the same language style and a similar length. [legitimate news article]
```

Statistics: 11941 (from 11941 legitimate)

Exmple:

```json
"gossipcop-842358": {
        "origin_id": "gossipcop-842358",
        "origin_label": "legitimate",
        "origin_text": "She's expecting her first child with husband-to-be Ryan Lochte.\n\nAnd Kayla Rae Reid spared no expense as she celebrated the impending arrival of their son with a lavish baby shower on Sunday.\n\nThe Playboy model was joined by friends and family for the bash at the Doheny Room in West Hollywood.\n\nScroll down for video\n\n'Oh boy!' Ryan Lochte's model love Kayla Rae Reid celebrates her baby shower with lavish party at the Doheny Room in West Hollywood on Sunday\n\n'With my mom and sister!' The 25-year-old shared pictures from the day to Instagram\n\nThe upmarket restaurant was transformed for the occasion, with blue and white decorations decking the interior.\n\nTouches of gold, a nod to her baby's Olympian father, added a sparkle, with balloons spelling out the words 'Oh baby' hung along one wall.\n\nThe 25-year-old shared pictures from the day to Instagram, posing alongside her mother and sister.\n\nSweet treats: The upmarket restaurant was transformed for the occasion, with blue and white decorations decking the interior\n\nTake a seat: White roses decorated the long dining table\n\n'With my mom and sister,' she wrote. 'Thank you @Vanessa_muah for doing such a great job on their makeup for my shower!'\n\nAnother image showed the mother-to-be posing behind a table, upon which sat her cushion-style cake, a golden crown balanced on top.\n\n'Thank you immensely to everyone who helped make my baby shower absolutely amazing!' she wrote.\n\nFor her shower Kayla wore a figure-hugging beige dress which highlighted her neat bump, throwing a long cream jacket over the top.\n\nParents to be: The Playboy model is expecting her first child with Olympian fiance Ryan Lochte\n\nRyan has previously expressed his delight at his impending fatherhood, with the 32-year-old making no attempt to hide his pleasure in the fact the child is a boy.\n\nHe said: 'We’re having a boy. I was [hoping for a boy] because I always wanted more than one kid and I definitely wanted a boy first so if we have a girl, the boy will be the big brother and take care of his sister so it’s working out perfectly.'\n\nThe two are planning their wedding for October.",
        "generated_text_glm4": "She's anticipating the arrival of her firstborn with her fiancé, swimmer Ryan Lochte.\n\nKayla Rae Reid went all out for the celebration of their child's upcoming debut, hosting an opulent baby shower on Saturday.\n\nThe model gathered with relatives and close friends at a venue in West Hollywood's Doheny Room.\n\nScroll down for footage\n\n'Excitement ahead!' Kayla Rae Reid, partner of Ryan Lochte, marks her baby shower with an extravagant event at the Doheny Room in West Hollywood on Saturday.\n\n'Amongst loved ones!' The 25-year-old shared moments from the event on her social media\n\nThe posh location received a makeover for the celebration, decked out in blue and silver trimmings.\n\nTouches of silver, a reference to the athlete dad-to-be, added a shimmer, with balloons arranged to spell 'Oh baby' along a wall.\n\nThe expectant mother posted snippets on Instagram, including ones with her and her female relatives.\n\nDelicious treats: The venue underwent a special transformation, adorned with blue and silver-themed decor\n\nDining elegance: Silver roses adorned the dining table\n\n'With my nearest and dearest,' she captioned. 'A big thanks to @Vanessa_muah for the stunning makeup at the shower!'\n\nIn another snap, she was captured standing by a table featuring her cake, topped with a regal silver tiara.\n\n'Massive gratitude to all who contributed to an unforgettable baby shower!' she expressed.\n\nFor the event, Kayla donned a form-fitting nude gown that accentuated her baby bump, layered with a flowing cream coat.\n\nSoon-to-be parents: The model and her Olympian fiancé are eagerly awaiting their first child\n\nRyan has publicly shared his excitement about becoming a dad, with the 32-year-old openly expressing his joy over having a son.\n\nHe shared, 'It’s a boy. I was [hoping for a boy], as I’ve always dreamt of having a family with more than one child. Having a son first is ideal, and if we then have a daughter, he can look after his little sister. It couldn’t be better planned.'\n\nThe couple has their wedding day set for later in the fall.",
        "has_top_img": 1
    },
```

## Integration-based Fake

Filename: gossipcop_v3-3_integration_based_fake_tn200.json

use [Neural Topic Model](https://github.com/zll17/Neural_Topic_Models) to extract hidden topics, and then construct topic-related document pairs to integrate.

Prompt:

For a pair of human-generated **fake** and **legitimate** news with similar topics or content as inputs:

```text
Amalgamate the following two articles into a new and cohesive article while keeping a similar length. [fake news article], [legitimate news article]
```

Statistics: 2697 (from 2697 legitimate and 2697 fake)

Example:

```json
"gossipcop-955764_gossipcop-254760936": {
        "doc_1_id": "gossipcop-955764",
        "doc_1_label": "legitimate",
        "doc_1_text": "Khloé Kardashian didn’t get what she wanted, and she’s glad about it. The new mom opened up to her Twitter followers about why she longed for her first child to be a boy.  Related: The Kardashian Family: Get to Know the Next Generation While making their mark on the entertainment and business world, the Kardashian-Jenner clan is also raising their next generation. Kourtney Kardashian was the first of Kris Jenner’s children to have kids of her own. Kourtney and her now-ex Scott Disick welcomed their eldest son, Mason, in December 2009, followed by daughter Penelope three years later. […]  I wanted a boy so badly Because Mason and I are so close. I love our bond. I felt confident in having a boy but God blessed me with my precious True and now I wouldn’t know what to do with a boy. True has made me sweeter and more gentle. God gives you what you need. My BFF 4Life — Khloé (@khloekardashian) July 28, 2018  “I wanted a boy so badly Because Mason and I are so close. I love our bond,” the Keeping Up With the Kardashians star tweeted on Saturday, July 28, referring to sister Kourtney Kardashian‘s eldest child. “I felt confident in having a boy but God blessed me with my precious True and now I wouldn’t know what to do with a boy. True has made me sweeter and more gentle. God gives you what you need. My BFF 4Life.”  Kardashian, 34, noted that True fits in well with the two cousins closest to her in age: Kim Kardashian’s 6-month-old daughter, Chicago, and Kylie Jenner’s 5-month-old little girl, Stormi. “ANDDDD she has her two cousins to be her besties,” she added. “We call them the triplets it’s just the cutest!! GOD IS GREAT.”  Related: True Thompson’s Baby Album: Khloe Kardashian and Tristan Thompson’s Firstborn Daughter Khloé Kardashian has been a doting mommy ever since her first baby with Tristan Thompson, daughter True, arrived in April 2018. True’s unique name was inspired by Kris Jenner’s grandfather and father. “I sometimes, still can’t believe I’m a mommy!!! True is the sweetest ever. I got my bestie for life! Thank you Jesus for […]  Fans will recall Khloé was disappointed when she learned the sex of her unborn child during a March episode of KUWTK. “I’m really hoping Kylie’s gonna say she’s lying and that I’m really having a boy,” she said after her youngest sister shared the news with her.  Meanwhile, she was completely honest on Saturday when a fan tweeted her to ask if her body bounced back after giving birth to True. “Hell no!! Lol i’m still working on it. And it will come in time … I hope LOL,” she quipped. “But sitting down I have a completely different stomach then I used to have LOL I really can’t even talk about it.”  When put on the spot about whether she thinks about having more children, the Good American founder — who welcomed her first child with boyfriend Tristan Thompson in April — was equally as forthcoming: “Not right now lol True is only 3 months old so give me some time lol.”  Related: Khloe Kardashian and Tristan Thompson Cheating Scandal: Everything We Know So Far Photos and videos surfaced of Khloé Kardashian’s boyfriend, Tristan Thompson, allegedly cheating on her with multiple women. Thank You! You have successfully subscribed. Subscribe to newsletters Subscribe By signing up, I agree to the Terms and Privacy Policy and to receive emails from USWeekly Deal of the Day Shine Bright in This Glistening Mesh Top for New […]  Over on her Instagram Story, Khloé enjoyed time with True, singing to her: “Good morning to you / Good morning to you / Good morning, sweet True/ Good morning to you,” before adding, “That’s your song.” The baby cooed and smiled as her mom serenaded her.  baby True 💗 A post shared by Kardashian Videos. (@kardashianvideos) on Jul 28, 2018 at 8:34am PDT  “I’m such a dork. I sing this song every morning to her,” the Revenge Body host elaborated on Twitter. “I think she looks forward to it but maybe that’s wishful thinking lol.”  While all seems well with mom and baby, the same cannot be said for Khloé’s relationship with Thompson, 27. (The NBA player was caught cheating on the reality star with multiple women while she was pregnant.) “Khloé and Tristan are still not fully OK,” a source revealed in the new issue of Us Weekly. “They act like they are when they’re in front of others, but it’s all a show at this point.”",
        "doc_2_id": "gossipcop-254760936",
        "doc_2_label": "fake",
        "doc_2_text": "Khloé Kardashian “went ballistic” when she found out her NBA baby daddy, Tristan Thompson, had played away with an Instagram model while he was in New York last weekend with the Cleveland Cavaliers.  A source close to the Kardashian family said pregnant Khloé, who is due to give birth to their daughter any day now, “was devastated when she saw the pictures of Tristan with that girl, she went absolutely ballistic at him. She is not only hurt, she is humiliated and worried for their child. How could he do this, and so publicly, when their baby daughter could arrive within a week?”  Nine-months-pregnant Khloé had remained at home in Cleveland while Thompson, whom she has been dating since 2016, traveled to New York last weekend ahead of the Cavs’ game against the Knicks at Madison Square Garden on Monday.  But, in photos obtained by Page Six on Tuesday, the baller was seen at his five-star hotel with Bronx Instagram model Lani Blair on Saturday.  Blair, who is also said to be a strip club bartender and bottle service waitress, spent four hours at Thompson’s hotel, The Four Seasons — according to witnesses — before they headed out together to private members club Soho House in the Meatpacking District on Saturday night.  Thompson and Blair were photographed returning together to his hotel at 5 a.m. Sunday. Blair was seen emerging hours later, at 8 p.m. Sunday, wearing the same clothes she’d had on the night before and clutching an overnight bag.  Online video also circulated of Thompson and Blair apparently kissing at a daytime party earlier Saturday at NYC rooftop hotspot PH-D. A source added to Page Six, “Apparently Tristan and Lani spent a lot of time together over the weekend.”  The Kardashian family has remained unusually silent on social media since the scandal broke on Tuesday, and their reps have not responded to requests for comment. Khloé’s personal rep has also not commented.  But a family source said that the Kardashians were not completely surprised by Thompson’s antics. “The truth is that he has a bad reputation, they had warned Khloé about him, he’s done this before. But she didn’t want to hear it, she loves him.”  Thompson already has a child, a son, with his ex Jordan Craig, who was born after he started dating Khloé.  Khloé had posted a touching photo of her and the NBA star kissing on Monday with the sweet caption to their baby, “We are ready whenever you are little mama.” The photo, along with other loving shots of her and Thompson, remained up on her Instagram page as of Wednesday.  Thompson is now back in Cleveland — and was believed to have been at home Tuesday when pictures emerged of him and the Instagram model — where the Cavaliers will face the Knicks again Wednesday night in the final game of the season.  Reps for the Cavaliers have not commented on behalf of Thompson, whose cheating sparked a massive backlash on social media.",
        "generated_text": "Khloé Kardashian recently found out that her boyfriend, Tristan Thompson, had cheated on her while he was in New York with the Cleveland Cavaliers. According to sources, the pregnant reality star was devastated when she saw pictures of Thompson with an Instagram model. She is not only hurt and humiliated, but she is also worried about their unborn child. Thompson, who already has a child with his ex Jordan Craig, was spotted at a hotel with the Instagram model Lani Blair on Saturday night. The pair spent several hours at the hotel before heading out to a private club. Online videos also circulated of Thompson and Blair kissing at a daytime party earlier that day. The Kardashian family has remained silent on social media since the scandal broke, but sources say that they were not completely surprised by Thompson's actions. Thompson is now back in Cleveland, where the Cavaliers will face the Knicks in their final game of the season. Khloé, on the other hand, is focusing on her new role as a mother to her six-month-old daughter True. In a recent tweet, she revealed that she wanted a boy because she is close to her sister Kourtney, who has a son named Mason. Despite the cheating scandal, Khloé says that True has made her sweeter and more gentle. She also admits that she is still working on her body after giving birth to True. As for having more children, Khloé says that she is not ready right now, as True is only three months old. Despite the challenges she has faced, Khloé remains optimistic and grateful for her life.",
        "has_top_img": 1
    },
```

## Story-based Fake

Filename: gossipcop_v3-4_story_based_fake.json

Prompt:

For both human-generated **fake** and **legitimate** news as inputs:

```text
Write a news article based on the following message and return the body content only. You must generate even if there is not enough information. \nMessage: [news article title]. \nBody Content:
```

Statistics: 15729 (from 11941 legitimate and 3784 fake)

Example:

```json
"gossipcop-8889799564": {
        "origin_id": "gossipcop-8889799564",
        "origin_label": "fake",
        "origin_text": "We don’t know whether you are from team Jennifer Anniston or team Brad Pitt, but this news has warmed most of the hearts. The ex-couple recent went through divorce with their respective spouses. Post that, the fans started joking about Jen-Brad reconciliation. However, this joke turned to reality real soon and the reports are rife that the two are dating. The latest piece of news around their relationship is that they might have a baby soon!\n\nA source told In Touch Weekly, \"His marriage [to Angelina Jolie] fell apart, then her marriage to Justin [Theroux] ended. During that difficult time, Brad and Jen reconnected. It's like destiny brought them together, and I can definitely see them having a child together.”\n\nThe source also added that the couple might try the IVF method. While Brad Pitt has six children with Angeline Jolie, this will be Jennifer’s first child. The source added, “\"Even if it meant months of trying IVF. When Jen sets her mind to something, she doesn't stop until she succeeds.” The source further went on to say that this is the ‘ultimate slap’ on Angelina’s face and that she is livid about their decision. \"They both have changed over the years and, after much heartache, are at a great place in their lives. Brad loves the idea of how they'd both come full circle and found each other again. Having a child together seems like the perfect next step, the source revealed.\n\nWell, we won’t mind believing this amazing piece of news for a while. After all, all the ‘Friends’ fanclubs dreamed about this day since ages!\n\n(The above story first appeared on LatestLY on May 11, 2018 01:48 PM IST. For more news and updates on politics, world, sports, entertainment and lifestyle, log on to our website latestly.com).",
        "origin_title": "Jennifer Aniston And Brad Pitt’s Decision to Have a Baby Leaves Angelina Jolie Furious?",
        "generated_text": "Jennifer Aniston and Brad Pitt's decision to have a baby has left Angelina Jolie furious, according to sources close to the actress. The couple, who have been dating for several months, reportedly decided to have a child together after discussing their options with a fertility specialist.\n\nAngelina, who is already mother to six children, is said to be devastated by the news. She is said to be jealous of Jennifer's youth and beauty, and is worried that the arrival of a new baby will further marginalize her in the spotlight.\n\nA source close to Angelina told Entertainment Tonight: \"Angelina is devastated. She loves Brad and she loves Jennifer, but she can't help but feel left out. She's always been the bridesmaid, and now Jennifer is going to be the bride with the baby.\"\n\nHowever, Jennifer and Brad have reportedly not informed Angelina of their decision to have a baby. The actress is said to be unaware of the news, and is believed to be feeling hurt and betrayed by the couple's actions.\n\nIt is unclear what the future holds for Jennifer and Brad's relationship, or whether Angelina will be able to reconcile with the actress. However, sources close to the actress have indicated that she is determined to move on and is focusing on her own happiness and well-being.",
        "has_top_img": 1
    }
```

## Style-based Legitimate

Filename: gossipcop_v3-5_style_based_legitimate.json

Prompt:

For human-generated **legitimate** news as inputs:

```text
Polish the following news article to make it more objective and professional. Do not change the original meaning. Do not add extra information or delete certain information. [legitimate news artical]
```

Statistics: 11945 (from 11945 legitimate)

Example:

```json
"gossipcop-541230": {
        "origin_id": "gossipcop-541230",
        "origin_label": "legitimate",
        "origin_text": "Born and raised in the Philippines, Lea Salonga grew up watching Disney movies and listening to Disney storybook tapes. Never did she imagine, though, that she would grow up to be a real-life, bona fide Disney Princess.\n\nThen, after earning a Tony Award for her portrayal of Kim in the Broadway musical “Miss Saigon” in 1991, Salonga landed the career break of a lifetime: to be the singing voice of Princess Jasmine in the 1992 hit Disney film “Aladdin.”\n\nSix years later, she got a second chance to live her young girl’s dream as she performed the vocals of Mulan in the 1998 Disney film of that name.\n\n“I never thought when I was 5 and listening to ‘Cinderella’ stories that I’d be a Disney princess. I think it’s such a magical thing to happen in my life, and for it to happen twice is something I would never have thought could happen,” said Salonga in a recent phone interview.\n\nSalonga’s distinctive voice will return to Southern California for concerts tonight at the Valley Performing Arts Center in Northridge and Saturday at Segerstrom Center for the Arts. Backed by a four-piece band, Salonga will perform a selection of well-known songs, including her greatest hits from her various musicals and films.\n\n“We made sure to choose a fun program that the band is going to dig playing and I’m going to love singing,” said Salonga, “and because we are having so much fun onstage, I hope that translates to the audience as well.”\n\nSalonga is keeping the program’s song selections a secret for now, until she and her musical director decide on the set list; however, she promises all of the tunes will be familiar and fit her vocal range. Some of the songs, she added, will be making their California debut.\n\n“This will be the first time for California audiences to hear these songs, but there is nothing unknown or out of left field; stuff that always makes sense with my voice.”\n\nA regular feature of Salonga’s solo concerts is an audience participation segment, in which she chooses someone to join her onstage to sing the Grammy and Academy Award-winning duet “A Whole New World” from “Aladdin.”\n\n“No need to panic; we always have a lyric sheet so anyone who dares to come up doesn’t have to have it memorized fully,” she said. “I want them to have fun.”\n\nSalonga has numerous Broadway credits, including her role as Eponine in the 1993 “Les Misérables” Broadway run and as Fantine in the 2006 Broadway revival. She recently came off Broadway in the new musical “Allegiance,” which also starred George Takei and Telly Leung.\n\nSplitting her time between the U.S. and Manila, Salonga is a coach on the Philippine version of the television show “The Voice.” In addition to her onscreen and onstage career, she has released several solo albums, including “I’d Like to Teach the World to Sing” (1997) and “By Heart” (1999).\n\nOn this tour, Grammy-nominated bass player Trey Henry and drummer Ray Brinker, both from the jazz group Tierney Sutton Band, will back Salonga.\n\n“I get to go up onstage with musicians who I really admire and respect, and just have a great time with,” Salonga said. “It’s thrilling when I get to perform stuff where I can just emotionally let go and fly off to another world in my mind, and the audience gets to ride on that too.”\n\nContact the writer: jmoe@ocregister.com",
        "generated_label": "legitimate",
        "generated_text_t015": "Lea Salonga, a native of the Philippines, has achieved her dream of becoming a Disney Princess. After earning a Tony Award for her portrayal of Kim in the Broadway musical \"Miss Saigon\" in 1991, Salonga landed the role of Princess Jasmine in the 1992 hit Disney film \"Aladdin.\" She later reprised her role as Mulan in the 1998 Disney film of the same name.\n\nIn a recent phone interview, Salonga reflected on the magical experience of becoming a Disney Princess. \"I never thought when I was 5 and listening to 'Cinderella' stories that I'd be a Disney princess,\" she said. \"I think it's such a magical thing to happen in my life, and for it to happen twice is something I would never have thought could happen.\"\n\nSalonga will perform a selection of well-known songs, including her greatest hits from various musicals and films, at concerts tonight at the Valley Performing Arts Center in Northridge and Saturday at Segerstrom Center for the Arts. She will be backed by a four-piece band.\n\n\"We made sure to choose a fun program that the band is going to dig playing and I'm going to love singing,\" Salonga said. \"And because we are having so much fun onstage, I hope that translates to the audience as well.\"\n\nSalonga's solo concerts often feature an audience participation segment, in which she chooses someone to join her onstage to sing the Grammy and Academy Award-winning duet \"A Whole New World\" from \"Aladdin.\" She promised that the audience will be familiar with the tunes and that they will fit her vocal range.\n\nSalonga has numerous Broadway credits, including her role as Eponine in the 1993 \"Les Misérables\" Broadway run and as Fantine in the 2006 Broadway revival. She recently came off Broadway in the new musical \"Allegiance,\" which also starred George Takei and Telly Leung.\n\nSplitting her time between the U.S. and Manila, Salonga is a coach on the Philippine version of the television show \"The Voice.\" In addition to her onscreen and onstage career, she has released several solo albums, including \"I'd Like to Teach the World to Sing\" (1997) and \"By Heart\" (1999).\n\nOn this tour, Grammy-nominated bass player Trey Henry and drummer Ray Brinker, both from the jazz group Tierney Sutton Band, will back Salonga. \"I get to go up onstage with musicians who I really admire and respect, and just have a great time with,\" Salonga said. \"It's thrilling when I get to perform stuff where I can just emotionally let go and fly off to another world in my mind, and the audience gets to ride on that too.\"\n\nContact the writer: [jmoe@ocregister.com](mailto:jmoe@ocregister.com)",
        "has_top_img": 1
    }
```

## Integration-based Legitimate

Filename: gossipcop_v3-7_integration_based_legitimate_tn300.json

Prompt:


For human-generated legitimate news with similar topics or content as inputs:

```text
Summarize the following two articles into a single, cohesive article, ensuring minimal loss of information without significantly shortening the overall length. [legitimate news article 1], [legitimate news article 2]
```

Statistics: 5926

Example:

```json
 "gossipcop-916405_gossipcop-905417": {
        "topic_id": 0,
        "topic_words": [
            "work",
            "movie",
            "Awards",
            "like",
            "say",
            "act",
            "mother",
            "Golden",
            "Pfeiffer",
            "actress",
            "role",
            "film",
            "tell",
            "german",
            "watch"
        ],
        "doc_1_id": "gossipcop-916405",
        "doc_1_label": "legitimate",
        "doc_1_text": "Tonya Harding says the Olympics have changed since she competed all those years ago.  Tonya Harding says the Olympics have changed since she competed all those years ago.  \"Wow, I'm so glad I'm not competing against them now,\" Harding says of the Olympic figure skaters, noting that the \"point system\" has changed. \"I was all about doing the triple axel or the triple-triple, and now you can do the triple-triple and still get the same points that you would for the triple axel. So, why do the triple axel?\"  Harding was the first American woman to successfully do a triple axel in a competition, and recalls the moment she knew she landed the move. \"I was like, 'Yes! I did this!'\" she says. \"I competed for me but I performed for the people.\"  Harding also remembers being at the Olympics and thinking, \"Holy crap.\"  \"Then you have to remember to bring yourself back down to a level that this is just another competition,\" she explains. \"You're like that for a bit and then you start to look around and you're like, 'Holy crap, this is the Olympics.'\"  Harding has found herself back in the limelight this year after the success of the movie I, Tonya, which is about her life as a figure skater. She tells DeGeneres that she's quite happy with how the film turned out.  \"I achieved something in my life that meant something,\" she says. \"With the new movie, it actually made my life feel like it was worth something.\"  In January, Harding joined the I, Tonya cast at the Golden Globes and celebrated with Allison Janney after she won for her portrayal of LaVona Golden, Harding's mother.  \"She was overwhelmed by the movie,\" Janney told ET's Kevin Frazier of Harding's reaction to the critically acclaimed film. \"I think she's having a great moment. I think she loves it and I think she should because the movie tells a more nuanced side of her story.\"  Janney added, \"It's much more complicated then what we first thought when this incident happened back in the '90s.\"  Check out more of our exclusive interview with the Golden Globe winner:",
        "doc_2_id": "gossipcop-905417",
        "doc_2_label": "legitimate",
        "doc_2_text": "Story highlights Margulies talks about life after Alicia Florrick The actress is currently working on a new film  CNN —  Julianna Margulies isn’t missing “The Good Wife,” just yet.  The actress, who just wrapped the series finale of her long running CBS drama in June, told CNN she’s only beginning to adjust to life after Alicia Florrick.  “I haven’t missed [the show] yet,” she told CNN at The ACE Awards in New York on Tuesday night. “We probably would be in our third week back at work now if I was still doing it. I really wonder, now that I have the time to think about it, how I did seven years of that show because just the legal dialogue alone. My mind was never still.”  Margulies said that right after she taped the last episode, she got sick. “I have been really actually wondering how I just kept going. So the exhaustion when it all finally ended, hit me with a bout of the chickenpox for two weeks. I felt like, sort of my body having to shut down and shed seven years of great hard work and start anew. I really took it that way.”  Related Link: ‘The Good Wife’ series finale reaches a frustrating verdict  Margulies, who has won two Emmy Awards for her work on “The Good Wife,” admitted that she was surprised the hit show wasn’t nominated this year.  “I thought this season was our strongest season, to be honest,” Margulies said. “It’s someone else’s turn. I’ve won plenty and I’ve been nominated plenty.”  Margulies didn’t pause long before for taking on a new role. She’ll play Richard Gere’s wife in the upcoming movie, “The Three Christs of Ypsilanti.” The film is already in production and Margulies said she’s enjoying her new gig.  “Oh, it’s heaven,” she said. “He is genuine, he’s not fussy [Gere]. After our first day, it was as if we had been married for 10 years already. He’s just lovely, I mean honestly, he’s truly a dream.”",
        "generated_label": "legitimate",
        "generated_text_t01": "Tonya Harding, the first American woman to successfully do a triple axel in a competition, reflects on the changes in the Olympics since she competed. She notes that the point system has changed, making it less advantageous to perform difficult moves like the triple axel. Harding also discusses her success with the movie I, Tonya, which has made her feel like her life has worth something. She recently joined the cast of the movie at the Golden Globes and celebrated with Allison Janney, who plays her mother in the film. Margulies, who recently wrapped the series finale of The Good Wife, talks about adjusting to life after the show and her upcoming role in the movie The Three Christs of Ypsilanti. She says that she's enjoying working with Richard Gere, who she describes as genuine and lovely.",
        "has_top_img": 1
}
```
