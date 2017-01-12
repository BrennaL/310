# Deliverable 0: Async Development

### We need to create your repo for this deliverable, these will be setup on Monday morning. You **MUST** register your GitHub username with the [ClassPortal](http://skaha.cs.ubc.ca:11310) for this to work.

Asynchronous development requires different programming idioms than synchronous development. This deliverable requires a set of asynchronous tasks be completed to calculate an end number. 

While you _could_ do this synchronously, later deliverables will not be possible synchronously so it is not to your benefit to try to work around this. Also, while you could complete this deliverable with nested callbacks, promises, or async/await, we require you to use promises.

This will be an individual deliverable (the only one in the project). It is worth 10% of your final grade. You will not have to hand anything in; we will pull from your D0 repository at noon on January 16, 2016. Before we can provision your D0 repository, you will have to alias your Github userid with your course account, please do so at [http://skaha.cs.ubc.ca:11310](http://skaha.cs.ubc.ca:11310). We will create project January 9 @ 0900. You do not need to specify your teammate until 0900 on January 16. We will run [MOSS](https://theory.stanford.edu/~aiken/moss/) on all submissions so please make sure your work is your own.

You are responsible for the software design and implementation that supports the API listed in ```src/Math.ts```. You cannot use any library package that is not already specified in ```package.json```. Your implementation must be in TypeScript and must compile without error. While we will not be directly examining your source code, you will undoubtably end up showing it to the TAs as you explain your solution in the deliverable retrospective.

The main API you will use for this deliverable is [```request-promise-native```](https://github.com/request/request-promise-native). This package will automatically be installed when you run ```yarn configure```. 

## Dataset

The primary API for this deliverable are:

* ```Math::add(urls: string[]): Promise<number>```
* ```Math::multiply(urls: string[]): Promise<number>```

The parameter takes a list of URLs, each of these URLs corresponds to a JSON file that looks optimally like (http://skaha.cs.ubc.ca:11313/4968.json):

```
[ 1, 2, 5, 4 ]
```

The math operations should only be on the numbers in arrays within the JSON file, e.g. for (http://skaha.cs.ubc.ca:11313/7b77.json):

```
{ "id": "foo", "bar": false, "baz": 6, "values": [1, 2, 3] }
```

Only 1, 2, 3 should be used. You only need to consider direct arrays (first example) or property value arrays (second example), but do not need to consider nested arrays: (e.g., (http://skaha.cs.ubc.ca:11313/822d.json) ```{"val": {"foo": [1, 2, 3]}}```). Also, only numbers should be considered (e.g., for ```[1, "2", 3]``` the ```2``` is a string and should not be considered).

```
add(['http://skaha.cs.ubc.ca:11313/822d.json']) -> reject('Error: No number was provided')

add(['http://skaha.cs.ubc.ca:11313/822d.json', 'http://skaha.cs.ubc.ca:11313/4968.json']) -> fulfill(12)

add([]) -> reject('Error: No number was provided')

add(['invalidURL']) -> reject('Error: URL could not be retrieved')

multiply(['http://skaha.cs.ubc.ca:11313/822d.json']) -> reject('Error: No number was provided')

multiply(['http://skaha.cs.ubc.ca:11313/822d.json', 'http://skaha.cs.ubc.ca:11313/4968.json']) -> fulfill(40)

multiply(['URLwithInvalidJSON']) -> reject('Error: Could not parse JSON')
```


## Testing

The best way to test your system is via your own unit test suite. You can write these unit tests by following the examples in ```test/``` and running them with ```yarn test```. This will be the quickest and easiest way to ensure your system is behaving correctly and to make sure regressions are not introduced as you proceed further in the project.

AutoTest can also be invoked every 12h by making a ```@CPSC310bot``` comment in a GitHub commit message; full details will be available in the [AutoTest](AutoTest.md) documentation.

The AutoTest suite will comprise 80% of your mark. The remaining 20% will be derived from your test coverage score for your files in ```src/```. You can check your score (as we will) by running ```yarn cover```. Your grade will correspond to the fraction your tests cover (e.g., 90% coverage will give you 18/20). Recognizing that hitting 100% will take more trouble than it is worth, we will give you a maximum 5% bonus for your coverage score, although you cannot get over 100% on this component. For example, if your coverage rate is 97% you will get 100%. If it is 76% you will get 81%. 

## Getting started

This deliverable is fairly straightforward but will involve a new language for most of you, along with a new tooling environment. Please do not delay getting started: the sooner you start, the more times you can invoke AutoTest on your solution.

It is important that you start by getting the code to compile and the existing tests to run. From there you can start to build out your solution. Getting hung up on language tutorials, articles, and Youtube videos is not the way to go with this deliverable.

Some URLS that you can use are: 
* http://skaha.cs.ubc.ca:11313/0.json
* http://skaha.cs.ubc.ca:11313/1.json
* http://skaha.cs.ubc.ca:11313/2.json
* http://skaha.cs.ubc.ca:11313/4543.json
* http://skaha.cs.ubc.ca:11313/4544.json
* http://skaha.cs.ubc.ca:11313/4666.json
* http://skaha.cs.ubc.ca:11313/4670.json
* http://skaha.cs.ubc.ca:11313/4968.json
* http://skaha.cs.ubc.ca:11313/4969.json
* http://skaha.cs.ubc.ca:11313/7b77.json
* http://skaha.cs.ubc.ca:11313/822d.json
* http://skaha.cs.ubc.ca:11313/944a.json
* http://skaha.cs.ubc.ca:11313/b43f.json
* http://skaha.cs.ubc.ca:11313/jdw3.json

Remember that our test suite will also use additional files so be sure to generate your own test data files as well.

