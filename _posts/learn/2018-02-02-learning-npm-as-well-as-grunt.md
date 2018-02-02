---
layout: learn
title: learning npm as well as grunt
date: 2018-02-02 12:26:26 +0800
categories: learning
tags: front-end
keywords: npm, grunt
---

# learning npm as well as grunt

<mark>Grunt</mark> is a task runner, which is based on nodejs, could have to do the repetitive tasks for developers
<mark>NPM</mark> is module package manager for nodejs



## diff between dependencies && devDependencies
- --save
- --save-dev

```

--save install dependency into dependencies into package.json
--save-dev install dependency into devDependencies

```

diff: the modules listing under devDependencies is for developer, which will not be deployed on the development env


grunt-contrib-concat is a plugin which could merge files together into one file, which could decrease the request times of https

one example could be:

{% highlight javascript linenos%}
module.exports = function(grunt) {

    // Project configuration.
    grunt.initConfig({

        concat: {
            "options": { "separator": " " },
            "build": {
                "src": ["hello.txt", "world.txt"],
                "dest": "helloworld.txt"
            }
        },
	   watch: {
		  files:['hello.txt', 'world.txt'],
		  tasks: ['concat'],
	   }

    });



    grunt.registerTask('default', ['concat']);
    grunt.registerTask('helloworld', ['concat']);
	grunt.registerTask('conwatch', ['watch']);

	grunt.loadNpmTasks('grunt-contrib-watch');
    grunt.loadNpmTasks('grunt-contrib-concat');

};

{% endhighlight %}

In this example, what codes try to do is to merge the content in hello.txt and content in world.txt into helloworld.txt.

grunt.initConfig is used to init and set property

<mark>    grunt.registerTask('default', ['concat']); </mark> is used to set the order of task

so the above code could be written like:

{% highlight javascript linenos%}
module.exports = function(grunt) {

    // Project configuration.
    grunt.initConfig({

        concat: {
            "options": { "separator": " " },
            "build": {
                "src": ["hello.txt", "world.txt"],
                "dest": "helloworld.txt"
            }
        },
	   watch: {
		  files:['hello.txt', 'world.txt'],
		  tasks: ['concat'],
	   }

    });



    grunt.registerTask('default', ['concat']);
    // grunt.registerTask('helloworld', ['concat']);
	// grunt.registerTask('conwatch', ['watch']);

	grunt.loadNpmTasks('grunt-contrib-watch');
    grunt.loadNpmTasks('grunt-contrib-concat');

};

{% endhighlight %}




