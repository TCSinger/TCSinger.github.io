{:.no_toc}
* toc
{:toc}

# Abstract

Zero-shot singing voice synthesis (SVS) with style transfer focuses on creating high-quality singing voices with unseen timbres and styles (like singing methods, rhythm, techniques, and pronunciation) from the prompt audio. However, the multifaceted nature of singing voice styles presents a substantial challenge for comprehensive modeling and effective transfer. Moreover, current zero-shot SVS models often fall short of generating singing voices with rich stylistic nuances. In light of these challenges, we propose a novel zero-shot SVS system TransferSinger, which primarily leverages three modules for enhanced effectiveness: 1) The style encoder that utilizes a VQ model to capture styles from the prompt audio. 2) The style and duration language model (S\&D-LM), which predicts style information and phoneme duration simultaneously, thereby enhancing both predictions. 3) The style adapt decoder that adapts mel-spectrograms using style information to generate singing voices with enhanced details. Our experimental results demonstrate that TransferSinger surpasses baseline models in both synthesis quality and singer similarity across various tasks: zero-shot SVS, controllable style synthesis, cross-lingual style transfer, and speech-to-singing style transfer.

---

# Zero-Shot SVS with Style Transfer

To assess the performance of TransferSinger and baseline models in the zero-shot SVS with style transfer task, we randomly select singing voices with unseen singers from the test set as target samples and different utterances from the same singers to form prompt samples.

1. Target: 

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
			<th style="text-align: center">Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/prompt/001.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/gt/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/yourtts/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/mega/001.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/rms/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/stye/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/trans/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2. Target: 

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
			<th style="text-align: center">Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/prompt/002.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/gt/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/yourtts/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/mega/002.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/rms/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/stye/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/trans/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

3. Target: 

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
			<th style="text-align: center">Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/prompt/003.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/gt/003.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/yourtts/003.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/mega/003.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/rms/003.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/stye/003.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/trans/003.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

4. Target: 

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
			<th style="text-align: center">Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/prompt/004.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/gt/004.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/yourtts/004.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/mega/004.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/rms/004.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/stye/004.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/trans/004.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

---

# Controllable Style Synthesis

We randomly select singing voice samples from the style-labeled testing sets of unseen singers and use these as prompt samples for the baseline models. Then, we use the style labels of these prompt samples as text prompts for TransferSinger to perform controllable style synthesis, with the timbre prompts also drawn from these prompt samples. Moreover, we randomly utilize content information from all songs in the dataset as the target.

1. Target: 
Style class: 

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/prompt/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/yourtts/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/mega/001.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/rms/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/stye/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/trans/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2. Target:
Style class:

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/prompt/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/yourtts/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/mega/002.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/rms/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/stye/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/trans/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

---

# Cross-Lingual Style Transfer

To test the cross-lingual style transfer performance of various models, we alternately use unseen Chinese and English data as prompts and targets for inference, using MOS and SMOS as evaluation criteria.

1. Target:
Chinese->English

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/prompt/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/yourtts/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/mega/001.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/rms/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/stye/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/trans/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2. Target:
English->Chinese

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/prompt/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/yourtts/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/mega/002.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/rms/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/stye/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/trans/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

---

# Speech-to-Singing Style Transfer

We conducted experiments on speech-to-singing style transfer and used MOS and SMOS to compare the performance of various models. To be specific, we used unseen speech audio as the prompt audio to transfer timbre and styles to the target singing voice. 

1. Target:

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/prompt/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/yourtts/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/mega/001.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/rms/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/stye/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/trans/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2. Target:

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/prompt/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
      		<th style="text-align: center">YourTTS</th>
			<th style="text-align: center">Mega-TTS</th>
			<th style="text-align: center">RMSSinger</th>
			<th style="text-align: center">StyleSinger</th>
			<th style="text-align: center">TransferSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/yourtts/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/mega/002.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/rms/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/stye/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/trans/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>
