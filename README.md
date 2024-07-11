# Second Opinion 🩺 (AI Code Review)

A github action which reviews your code


### Runing second-opinion.py

In isolation, the script takes a file containing differences, and sends it to chatgpt with some prompt information to get back the review. it writes the review to stdout.

You can easily test this script in your own python environment.

Navigate to the python directory:

```sh
    cd python
```

Install the dependencies:

```sh
    pip install -r requirements.txt
```

Set your OPENAI key:

```sh
    export AZURE_OPENAI_API_KEY=<your key>
```

generate a diff:

```sh
    git diff --no-prefix -U2000 --output diff.txt HEAD^1 HEAD
```

and then run the script.

```sh
    python second-opinion.py diff.txt
```



### Running in docker

To allow for this to run on environments without python setup (and as a prerequisite to creating a github action) there is also a docker image

(make sure you are in the root directory of the project before running these commands)

To build the image:

```sh
    docker build . -t seco
```

Generate a diff

```sh
    git diff --no-prefix -U2000 --output diff.txt HEAD^1 HEAD
```

To run the image (this mounts a file called diff.txt into the root of the container before calling second-opinion.py with diff.txt as an argument)

```sh
    docker run -it -v $(pwd)/diff.txt:/usr/src/app/diff.txt:ro --rm -e AZURE_OPENAI_API_KEY=<your api key> seco diff.txt
```
