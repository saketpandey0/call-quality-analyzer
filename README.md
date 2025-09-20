# call-quality-analyzer

Approach: 
This Call Quality Analyzer is designed to process sales call recordings 
efficiently in Google Colab’s free tier while staying within a 30-second 
runtime. The system follows a lightweight yet effective pipeline. 
First, the audio is preprocessed using librosa for normalization. If the 
recording is stereo (agent on one channel, customer on the other), talk
time ratio and monologues can be calculated directly. If mono, transcript
based approximations are used, while acknowledging that production 
systems would require speaker diarization (pyannote.audio). 
Speech-to-text transcription is performed with Whisper tiny.en, chosen 
for its speed and robustness to noisy inputs. This produces the 
conversation transcript, which is then analyzed to estimate the number 
of questions asked. Instead of relying on punctuation, the system 
detects question phrases such as “what,” “how,” “do you,” or “can you,” 
which better reflect spoken conversation. 
For sentiment, we use HuggingFace’s DistilBERT classifier to determine 
whether the overall tone is positive, negative, or neutral. From these 
metrics, the system generates one actionable insight, such as “customer 
showed repeated negative sentiment” or “agent dominated the call.” 
This approach balances accuracy and runtime efficiency, delivering 
meaningful insights within Colab’s constraints.
