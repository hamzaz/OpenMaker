<img src="https://github.com/openmaker-eu/socialmedia/blob/master/OpenMakerLogo.png" height="128"><img src="./figures/uzh_logo.png" height="100"><img src="https://github.com/openmaker-eu/socialmedia/blob/master/Ekran%20Resmi%202017-01-11%2014.34.43.png" height="128">

# The OpenMaker Opinion Leaders API

This API is a prototype of a feature where OM-DSP users could be able to detect and explore the opinion leaders within the maker community.

The fetaure provided by this API could also enable the DSP leaders or accelarators to explore and follow other makers with specific non-technical concerns or focuses.

The API may enable the accelarators or other users of the DSP to check any Tweeter user's 'influence' on open-making related themes as well as be able to see their possible position on the opinion score board. 

The API connects to the WatchTower APP and retrieves the list of influencers. It also connects to Twitter API to retrieve tweets of the designated influencers. It analyzes the textual contents of the latest tweets of the WatchTower influencers' as well as any other designated Twitter user.

## 1. The OpenMaker Opinion Leaders APP
A Jupyter notebook on the APP it self can be accessed [hereby](./OMLeaders.ipynb)

## 2. Running this API on a local computer

After having created the python environment using the [requirements file](./requirements.txt), run the python script which is given via this repository.

Check follwing guides for creation of pyhton environments: 
- http://stackoverflow.com/questions/7225900/how-to-pip-install-packages-according-to-requirements-txt-from-a-local-directory
- http://python-guide-pt-br.readthedocs.io/en/latest/dev/virtualenvs/

Once the repository installed on a local computer, replace the "https://openmaker.herokuapp.com/" part of the URL below with http://127.0.0.1:5000/
 
````
python run_wsgi.py
````

## 3. The server URL of the API

https://openmaker.herokuapp.com/

This returns the list of available category in json format:
````
{
  "categories": [
    "openness", 
    "sharing", 
    "innovation", 
    "sustainability", 
    "collectiveness"
  ], 
  "status": "OpenMaker.EU meme analysis server is UP."
}
````
## 4. Retrieving the list of opinion leaders

### Retrieving the list of overall opinion leaders on OpenMaking: 

https://openmaker.herokuapp.com/scoreboard

The score at the moment is generated using a built-in dictionary, where a predetermined keywords and phrases are matched to categories. The app aims to maximize accuracy and retrieval at detecting the predetermined expresions within the texts that are generated by an influencer. Right now, it scans the tweets of the user as input texts in order to detect themes within them and map the themes to the categories.

### Retrieveing the list of opinion leaders on a specific theme:

https://openmaker.herokuapp.com/scoreboard/sustainability

Checking ,for instance, the scoreboard of the sustainability debators. Sustainability is discussions/tweets on environmental sustainability issues. 

The general structure of access to a specific board is as follows:
````
https://openmaker.herokuapp.com/scoreboard/<category>
````

````
<category>:{"openness","sharing","innovation","sustainability", "collectiveness"}
````
## 5. Checking overall score of an influencer

The API provides the query option to be able retrieve the score of a particular influencer determined by the WatchTower APP or any othe Tweeter user:

https://openmaker.herokuapp.com/influencer/instructables
````
{
  "compositions": {
    "innovation": 0.14754098360655737, 
    "making": 0.5081967213114754, 
    "openness": 0.00546448087431694, 
    "sharing": 0.01639344262295082, 
    "sustainability": 0.02185792349726776
  }, 
  "influencer": "instructables", 
  "ntweets": 183, 
  "openmakership": 0.6994535519125683
}
````

Following query retrieves the score of a possible opinion leader who was not detected via the OpenWatcher:

https://openmaker.herokuapp.com/influencer/indy_johar
````
{
  "compositions": {
    "collectiveness": 0.025510204081632654, 
    "innovation": 0.08163265306122448, 
    "making": 0.3979591836734694, 
    "openness": 0.04591836734693878, 
    "sharing": 0.025510204081632654, 
    "sustainability": 0.025510204081632654
  }, 
  "influencer": "indy_johar", 
  "ntweets": 196, 
  "openmakership": 0.6020408163265306
}
````
The location of the queried user can be checked on the scoreboard of 'openness' for example:

https://openmaker.herokuapp.com/scoreboard/sharing
```
{
  "rankings": [
    {
      "score": 0.10050251256281408, 
      "username": "arduinoblog"
    }, 
    {
      "score": 0.08854166666666667, 
      "username": "shapeways"
    }, 
    ...
    {
      "score": 0.055, 
      "username": "Ultimaker"
    }, 
    {
      "score": 0.045454545454545456, 
      "username": "makerbot"
    },    
    {
      "score": 0.038461538461538464, 
      "username": "hamzaz"
    }, 
    {
      "score": 0.03783783783783784, 
      "username": "Raspberry_Pi"
    }, 
    {
      "score": 0.030303030303030304, 
      "username": "BarackObama"
    }, 
    {
      "score": 0.028901734104046242, 
      "username": "mbanzi"
    }, 
    {
      "score": 0.025510204081632654, 
      "username": "indy_johar"
    }, 
    ...
    {
      "score": 0.005025125628140704, 
      "username": "androidcentral"
    }
  ], 
  "type": "sharing"
}
````
It should be noted that any tweeter username can be queried by follwing pattern:

````
https://openmaker.herokuapp.com/influencer/<username>
````

