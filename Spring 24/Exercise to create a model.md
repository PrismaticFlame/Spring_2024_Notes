Uh... 'fun' exercise: Predict Suicidality from Tweets on Twitter.
- Goal: Predict which Twitter users are likely to attempt suicide
- Data: Tweets from many different users over time
	- Twitter profiles contain structured information
		- Log-on times, Log-on server location, profile name, profile picture
	- Tweets contain unstructured information
		- The text of the tweets
	- Tweets may contain images
### Potential Features
- "Suicide" -> binary (If they said "suicide" that is a strong indicator)
- Time in last month on Twitter -> Numeric
- Tone change
- Tweet Frequency
- Time of day/ratio @ night (Difficult because Twitter is worldwide)

### Features offered by Dr. Henry
- Time of day/night
- Country the user is from because countries have different suicide rates

### Feature Engineering with Unstructured Data
- Isolated users may be more depressed
	- Estimate sociability by number of tweets at people
	- May also combine with structured
- Users who use depressive language may be more depressed
	- Convert tweets to a positive/negative language score
- Certain profile pictures are indicative of depression
	- Determine the primary colors of the picture. Bright colored pictures are negatively correlated with depression. Black and white positively
