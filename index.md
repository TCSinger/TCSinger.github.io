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
			<th style="text-align: center">GT</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/prompt/001.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/ref/001.wav" type="audio/wav"></audio></td>
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
			<th style="text-align: center">GT</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/prompt/002.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/ref/002.wav" type="audio/wav"></audio></td>
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

---
