# Methodology and Code - NYT Weasel Bot: Sniffing Out Sourcing
A twitter bot scans The New York Times articles from the politics section for “weasel words,” then tweets out a link to the articles in which 3 or more “weasel phrases/words” are used, along with a snarky message designed to reflect the importance of adhering to the Society of Professional Journalists’ code of ethics. In addition, it tweets daily and weekly statistics, summarizing how “weasely” certain articles were.
# Methodology
The bot had to be designed in such a way that it could read all politics stories published every day, and tweet the articles which contained many weasel words. It also had to retain historical data to be able to tweet a summary at the end of every week. To achieve this, the bot takes 7 critical steps and tweets the article URL –
1.	Extract all URLs from the NYT politics page.

2.	Retain only those URLs that are truly related to politics. Through preliminary analysis, we determined the URL format used by The New York Times to represent politics stories and used the string to match the right URLs.

3.	Extract article content from each URL using Python’s ‘BeautifulSoup’ library. Specifically, it extracts the paragraph HTML tag.

4.	Remove the smaller articles from our list. This was because the small articles were primarily interactive visualizations with minimal text. Analyzing these would skew our results since weasel words are not expected in them.

5.	Process the text and clean it. This was required to ensure that the weasel words can be matched accurately. Through the cleaning processes the bot replaces words like ‘we’re’ by ‘we are’ and also handled punctuation, double spaces and special characters.

6.	It then looks for weasel words in the article text and increments the counter by one each time it finds it in the article. These counts are stored in a dataframe along with the article URL.

7.	Based on the number of weasel words, it then tweets the article and a short text alerting the reader of weasel words in the article. A jinja template has been used to produce variability in the text.

The bot tweets the total number of weasel words that were present in all articles published on a given day. At the end of every week, it tweets a summary for the entire week and also attaches the story with the maximum number of weasel words.
