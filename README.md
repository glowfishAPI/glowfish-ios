
glowfi.sh in iOS for the Big Web: Now with machine guns and rocket launchers.
-----------

**Installation**

    Download Glowfish.swift and drop it in your app...seriously, that's it.
    Also, make sure to get the amazing framework https://github.com/Alamofire/Alamofire which is used for our framework.

**Setup**

    Glowfish.setCredentials('<GLOWFISH_SID>', '<GLOWFISH_AUTH_TOKEN>');

**Useage**

Get ready for some simple machine learning...

*Training*

    Glowfish.train(data: [
	    "feature_name1": [1, 2, 3, 4, ...etc],
	    "feature_name2": [9, 4, 5, 6, ...etc]
    ], response: [
	    "class": [4, 3, 5, 6, ...etc]
    ])

*Predict*
It's important to note that predicting will throw an error if you have not trained against a data set first.

    Glowfish.predict(data: [
	    "feature_name1": [1, 2, 3, 4, ...etc],
	    "feature_name2": [9, 4, 5, 6, ...etc]
    ])

*Clustering*

    Glowfish.cluster(data: [
	    "feature_name1": [1, 2, 3, 4, ...etc],
	    "feature_name2": [9, 4, 5, 6, ...etc]
    ])

*Feature Selection*

    Glowfish.feature_select(data: [
	    "feature_name1": [1, 2, 3, 4, ...etc],
	    "feature_name2": [9, 4, 5, 6, ...etc]
    ], response: [
	    "class": [4, 3, 5, 6, ...etc]
    ])

**Further Documentation**

Docs - http://glowfish.readme.io/  
Registration - http://glowfi.sh/

**Thank You**

Thanks so much to Matt Thompson (@matt) for creating Alamofire. Big props.
