## nemo-saucelabs

### Installation

```npm install nemo-saucelabs --save-dev```

Add dependencies to package.json and install.

```javascript
	...
    "nemo": "^0.4.0",
    "nemo-saucelabs": "^0.1.3",
	...
```

### Configuration

Add nemo-saucelabs to your `config/nemo-plugins.json` file. 

```javascript
{
	"plugins": {
		"nemo-saucelabs": {
			"module": "nemo-saucelabs"
			"register": true
		}
	}
}
```

Define sauce labs `username` and `accessKey` to the config.json under `serverCaps` and register the plugin

```javascript
"serverCaps": {
    "username": "shop",
    "accessKey": "ei930kff-308c-49KK-6372-cfe251be-3j23", //not a real accessKey
    "sauceLabsRestApiUrl": " https://saucelabs.com/rest/v1/shop/jobs/",
    "idle-timeout": 300,
    "platform": "MAC",
    "version": "27.0"
  },
```

### Details

Once `nemo-saucelabs` plugin is registered, you will have `nemo.saucelabs` object available. `nemo.saucelabs` exposes methods called `updateJob` and `isJobPassed` to help update saucelabs test job and test results.


### Methods

<h5 class="name" id="allDisabled"><span class="type-signature"></span>1. updateJob<span class="signature">(data, callback)</span>

<dt>
<h6 class="name" id="allDisabled"><span class="type-signature">Request Fields for 'updateJob' method</span> 
```javascript
    name: [string] update the job name,
    cucumber_tags: [scenario.getTags()] nemo-sauce will traverse cucumber tags and get tag names to update the job tags
    tags: [list of strings] array of tags to update the job tags,
    build: [int] The build number being tested,
    custom-data: [JSON] a set of key-value pairs with any extra info that a user would like to add to the job. Max 64KB.
```

<h6 class="name" id="allDisabled"><span class="type-signature">Example</span> 
```javascript
@Before:
nemo.saucelabs.updateJob({  name: scenario.getName(),
                            cucumber_tags: scenario.getTags(),
                            build: build_id,
                            custom-data: {testInfo: 'information about test or cause of test failure...'}
                          }, callback);
```
</dt>

<h5 class="name" id="allDisabled"><span class="type-signature"></span>2. isJobPassed<span class="signature">(isPassed, callback)</span>

<h6 class="name" id="allDisabled"><span class="type-signature">Request Fields for 'isJobPassed' method</span> 
```javascript
    passed: [boolean] test result
```

<h6 class="name" id="allDisabled"><span class="type-signature">Example</span> 
```javascript
@After:
nemo.saucelabs.isJobPassed(!scenario.isFailed(), callback);
```

</dt>

<h5 class="name" id="allDisabled"><span class="type-signature"></span>3. getJobUrl<span class="signature">()</span>

<h6 class="name" id="allDisabled"><span class="type-signature">Example</span> 
```javascript
@After:
nemo.saucelabs.getJobUrl();
//e.g. https://saucelabs.com/tests/153a38fac7ab48869e7b3b9c3c567665, can be printed on report for reference
```