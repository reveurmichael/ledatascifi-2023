## How to measure "risk" in a 10-K

So you need to create variables describing risks a firm faces. At this point in the class, you probably aren't aware of any sophisticated language techniques, and that's fine! Simply counting how many times the 10-K discusses the "risk" (e.g. patent litigation) probably suffices. 

So, here's how I would build this code up:

1. As if you were inside the loop you set up to go over the files you downloaded, pick just one firm, and open its file as a string variable.
1. Clean that string, because it contains lots of HTML tags and in general has lots of non-word characters.
    - See notes from class on how to do this and/or look through the textbook 
    - Only proceed when you have this working well. 
1. Now you can try to define one "risk". 

    **Here are the coding mechanics of this:** Let's, for example, say I'm looking for discussions of losers and I'll save it in a new variable called `losers` added into my initial dataset: 
   - In this example, I think that if "DETROIT" is near "LIONS", the document is talking about losers. 
   - IMPORTANT: I have to see both words near each other to be sure it is about losers! If the document is just talking about Lions, it might be about animals, and if it is just talking about Detroit, it is talking about the economic engine of our great country, but if both words are close, the document is talking about losing and losers. _God, why am I a Lions fan? What have I done to foresake you?_
   - I define a regex pattern that looks for the word "detroit" near "loser". We talked about how to do this in class: Use `NEAR_regex`. Let's call that pattern `loser_regex_pattern`.
   - `hits = len(re.findall(loser_regex_pattern,<clean_10_text>))` will count the number of times the document discusses losing and save it to `hits`.
   - Save `hits` inside of the variable `losers` for that document (put it in the correct row!)  
   - **Manually check it by opening the 10-K on the browser - do your functions give you the same values you'd create if you did it by hand?**

    **So how should you define the regex pattern?**
    - You could just count how many times the risk word is used. But _be careful: You might need to make sure the topic is being discussed in the context (near) of risk. E.g. "Patent" is often talked about without invoking risks._
    - So, use `NEAR_regex()`. You give it a list like `[string1, string2]` and it will design a regex that looks for the strings being within some number of words of each other.
    - _Be careful: Sometimes the risk is discussed using a synonym or a partial word. E.g. the string "patents" is not the same to a computer as "patent"._
    - Advanced: What do you think `[(drake|billie eilish), (grammy|grammies|oscar|oscars)]` will do if used in the `NEAR_regex` function? (Go ahead and try it out!)
 
1. Repeat the steps in step 3 above to define that risk a second way, but change the words and parameters you used.
1. Repeat the steps in  step 3 above to define that risk a third way, but change the words and parameters you used.
1. Repeat the steps in  step 3 above to define a second type of risk.
    - Open some 10-Ks manually and read them to verify if your guess for how to check actually results in hits.
    - If it doens't work like you think (misses obvious discussions of the risk, or finds non-discussions), tweak it.
1. Repeat the steps in #3 above to define a third type of risk.
    - Open some 10-Ks manually and read them to verify if your guess for how to check actually results in hits.
    - If it doens't work like you think (misses obvious discussions of the risk, or finds non-discussions), tweak it.
1. Now, loop over all the firms and for each, measure the risks in the corresponding 10-K. _Warning: Looping over rows in a pandas dataframe is a little different than normal! Look up how to do it!_
    
    **IMPORTANT! `.describe()` those five variables after you're done!**
    - You should have observations for most/all firms for your new measures. **Fix it - do not proceed!**
    - If any of your variables are always 0, it's meaningless. **Change it - do not proceed!**
    - If any of your variables are always really high, consider if your search thinks too many things are that risk. Searching for "risk" for example is too vague. 
    
## Some more pointers on how to measure risk 

- Risks you could look to measure include, but are not limited to: antitrust; litigation - e.g. patent, consumer, class action; real estate; inflation; commodity; supply chain; natural disasters; weather; employees (fraud, compensation, departure); changes in tax policy; currency rates; regulatory approval; reputation; refinancing; 
- Prof. Kathleen Hanley [has a recent paper](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2792943) on risks. It focuses on financial firms, which isn't our sample, but nevertheless, it contains a long list of risks in Table 5 you might find interesting.

```{tip}
This assignment is about covid. What factors of firms do you think might make a firm more or less resilient to operating in a pandemic?
```
