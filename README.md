# Sentiment analysis (by Mattia Atzeni)
[🡅 TOP](#zaga)

NAO/Zora can automatically understand the **polarity** of what the user says. Based on the sentiment, the robot will make a neutral, positive or negative animation.

#### Prerequisites
1. [Apache Maven](https://maven.apache.org/download.cgi)  needs to be installed.
1. Download [glove.6B](http://nlp.stanford.edu/data/glove.6B.zip) and place all the text files into `WordVectors/glove.6B/`
1. Download SentiWordNet_3.0 in the root of the porject
```
wget -O SentiWordNet_3.0.txt https://github.com/aesuli/SentiWordNet/raw/master/data/SentiWordNet_3.0.0.txt
```
4. Download opennlp files
```
cd BUPPolarityDetection/opennlp/ &&\
wget http://opennlp.sourceforge.net/models-1.5/en-ner-date.bin &&\
wget http://opennlp.sourceforge.net/models-1.5/en-ner-location.bin &&\
wget http://opennlp.sourceforge.net/models-1.5/en-ner-organization.bin &&\
wget http://opennlp.sourceforge.net/models-1.5/en-parser-chunking.bin &&\
wget http://opennlp.sourceforge.net/models-1.5/en-pos-maxent.bin &&\
wget http://opennlp.sourceforge.net/models-1.5/en-pos-perceptron.bin &&\
wget http://opennlp.sourceforge.net/models-1.5/en-sent.bin &&\
wget http://opennlp.sourceforge.net/models-1.5/en-token.bin &&\
wget https://github.com/aciapetti/opennlp-italian-models/raw/master/models/it/it-pos-maxent.bin &&\
wget https://github.com/aciapetti/opennlp-italian-models/raw/master/models/it/it-pos_perceptron.bin &&\
wget https://github.com/aciapetti/opennlp-italian-models/blob/master/models/it/it-sent.bin &&\
wget https://github.com/aciapetti/opennlp-italian-models/blob/master/models/it/it-token.bin
```
5. Export Maven opts
```
echo 'export MAVEN_OPTS="-Xmx2G -Dorg.bytedeco.javacpp.maxbytes=10G -Dorg.bytedeco.javacpp.maxphysicalbytes=10G"' >> ~/.bashrc &&\
source ~/.bashrc
```

#### Usage with NAO/Zora
1. Go in the root of the project
1. Start the polarity detection service. `<PATH_TO_MAVEN>` should be changed with the directory to the local installed Maven.
```
cd ZoraSA/BUPPolarityDetection/  && \
<PATH_TO_MAVEN>/bin/mvn jetty:run -Djetty.http.port=8080
```
2.  Open the Choregraphe project, right click on the **SA** box, click **Set parameter** and set as **URL** the url of the preceded server (something like `http://<IP>:8080/sa/service`, where IP is the internet address of the computer where Jetty is running)
1.  Start the behavior, and after been said `Hey Zora`, wait for the beep and for eyes becoming blue, and say `execute sentiment analysis`
1.  Say or write in the dialog box the text