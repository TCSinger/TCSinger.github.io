{:.no_toc}
* toc
{:toc}

# Abstract

Zero-shot singing voice synthesis (SVS) with style transfer and style control aims to generate high-quality singing voices with unseen timbres and styles (including singing method, emotion, rhythm, techniques, and pronunciation) from audio and text prompts. 
However, the multifaceted nature of singing voice styles poses a significant challenge for comprehensive modeling and effective transfer and control. 
Furthermore, existing SVS models often fail to generate singing voices with a wealth of stylistic nuances for unseen singers. 
In this paper, we introduce TCSinger, a novel zero-shot SVS model that primarily employs three modules to address these challenges: 
1) the clustering style encoder that employs a clustering vector quantization (CVQ) model to condense style information into a compact latent space, thus facilitating subsequent predictions;
2) the Style and Duration Language Model (S\&D-LM), which concurrently predicts style information and phoneme duration, thereby enhancing both, and the S\&D-LM uses audio and text prompts to conduct both style transfer and style control;
and 3) the style adaptive decoder using a novel mel-style adaptive normalization method to generate singing voices with enhanced details.
Experimental results show that TCSinger outperforms baseline models in synthesis quality, 
singer similarity, and style controllability across various tasks, including zero-shot style transfer, multi-level style control, cross-lingual style transfer, and speech-to-singing style transfer.

---

**Note：** The audio on this GitHub page may load slowly and could pause momentarily at around the 2-second mark.Thank you for your patience.

---

# Zero-Shot Style Transfer

To assess the performance of TCSinger and baseline models in the zero-shot style transfer task, we randomly select singing voices with unseen singers from the test set as target samples and different utterances from the same singers to form prompt samples.

1.Target: 又 站 在 你 家 的 门 口 我 们 重 复 沉 默

Prompt: 终 于 你 开 口 向 我 诉 说 她 有 多 温 柔

Successfully transferring the timbre, resonance in pop singing method, mixed voice technique, pronunciation, rhythm, and pitch transition style.

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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/yourtts/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/mega/001.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/rms/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/style/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/trans/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2.Target: 我 听 见 雨 滴 落 在 青 青 草 地 SP 我 听 见 远 方 下 课 钟 声 响 起

Prompt: 可 是 我 没 有 听 见 你 的 声 音 SP 认 真 呼 唤 我 姓 名

Successfully transferring the timbre, pronunciation, pitch transition style, and rhythm.

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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/yourtts/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/mega/002.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/rms/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/style/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/trans/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

3.Target: 也 不 是 真 的 AP 不 会 想 你 AP 全 都 不 是 真 的 AP 是 骗 自 己

Prompt: 让 我 这 样 吧 SP 并 不 是 真 的 AP 路 过 而 已

Successfully transferring the timbre, pronunciation, pitch transition style, and rhythm.

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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/yourtts/003.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/mega/003.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/rms/003.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/style/003.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/trans/003.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

4.Target: 谁 娶 了 多 愁 善 感 的 你

Prompt: 谁 把 你 的 长 发 盘 起

Successfully transferring the timbre, pronunciation, pitch transition style, and rhythm.

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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/yourtts/004.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/mega/004.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/rms/004.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/style/004.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/svs/trans/004.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

---

# Multi-Level Style Control

## Parallel Style Control

In the parallel experiments, we use the GT global style and phoneme-level techniques as the target. 

## Non-Parallel Style Control

In the non-parallel experiments, global styles and six techniques are randomly yet appropriately assigned.

1.Target: 你 是 魔 鬼 中 的 天 使 所 以 送 我 心 碎 的 方 式 AP 是 让 我 笑 到 最 后

Timbre Prompt: 争 不 过 朝 夕 又 念 着 往 昔 偷 走 了 青 丝 却 留 住 一 个 你 岁 月 是 一 场 有 去 无 回 的 旅 行

Text Prompt: tenor bel canto

Successfully synthesizing the timbre, resonance in tenor bel canto singing method, the technique of falsetto and weak mixed voice, the articulation method, pronunciation, pitch transition style, and rhythm.


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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/yourtts/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/mega/001.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/rms/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/style/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/trans/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2.Target: AP 我 遇 见 谁 会 有 怎 样 的 对 白 AP 我 等 的 人 他 在 多 远 的 未 来

Timbre Prompt: AP 你 我 约 定 难 过 的 往 事 不 许 提 AP 也 答 应 永 远 不 让 对 方 担 心

Text Prompt: soprano pop

Successfully synthesizing the timbre, resonance in soprano pop singing method, the technique of falsetto and weak mixed voice, the articulation method, pronunciation, pitch transition style, and rhythm.

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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/yourtts/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/mega/002.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/rms/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/style/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/trans/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

---

**We also provide some demos that include only the effects generated by TCSinger using text prompts that incorporate certain techniques.**

3.Target: 宁 愿 选 择 留 恋 不 放 手 AP 等 到 风 景 都 看 透 AP 也 许 你 会 陪 我 看 细 水 AP 长 流

Timbre Prompt: 永 远 的 爱 我 SP 以 前 的 一 句 话 是 我 们 以 后 的 伤 口

Text Prompt: soprano pop falsetto

Successfully synthesizing the timbre of the timbre prompt, and refer to the text prompt, successfully synthesizing the resonance in soprano pop singing method and the technique of falsetto.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/prompt/003.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/trans/003.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

4.Target: 也 冷 却 了 我 手 中 的 鲜 花

Timbre Prompt: 好想再回到那些年的时光 AP 回到教室座位前后 AP

Text Prompt: alto pop vibrato

Successfully synthesizing the timbre of the timbre prompt, and refer to the text prompt, successfully synthesizing the resonance in soprano pop singing method and the technique of vibrato.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/prompt/004.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/text/trans/004.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

---

# Cross-Lingual Style Transfer

To test the cross-lingual style transfer performance of various models, we alternately use unseen Chinese and English data as prompts and targets for inference, using MOS and SMOS as evaluation criteria.

1.Target: I love you baby SP trust in me when I say

Prompt: 让 我 掉 下 眼 泪 的 不 止 昨 夜 的 酒

Language: Chinese->English

Successfully transferring the timbre, the articulation method, pronunciation, pitch transition style, and rhythm.

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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/yourtts/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/mega/001.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/rms/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/style/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/trans/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2.Target: 情 丝 百 转 丝 丝 缠 乱 犹 不 知 

Prompt: They've all been said before you know so why don't we AP just play pretend AP

Language: English->Chinese

Successfully transferring the timbre, the articulation method, pronunciation, pitch transition style, and rhythm.

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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/yourtts/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/mega/002.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/rms/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/style/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/cross/trans/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

---

# Speech-to-Singing Style Transfer

## Parallel Speech-to-Singing Style Transfer

In parallel experiments, we randomly select samples with unseen singers from the test set as targets and different speech from the same singers to form prompts.

1.Target: You make me happy AP when skies are gray

Prompt: I belive that the heart does go on

Successfully transferring the timbre, pronunciation, pitch transition style, and rhythm.

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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/yourtts/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/mega/001.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/rms/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/style/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/trans/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2.Target: It can happen to anyone of us anyone you think of

Prompt: And you wonder SP I wonder how I wonder why

Successfully transferring the timbre, the articulation method, pronunciation, pitch transition style, and rhythm.

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
			<th style="text-align: center">TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/yourtts/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/mega/002.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/rms/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/style/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/sts/trans/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

## Cross-Lingual Speech-to-Singing Style Transfer

In cross-lingual experiments, we select the speech prompt in a different lyric language from the target.

---

# Ablation Study

we undertake ablation studies to showcase the efficacy of various designs incorporated within TCSinger. SAD denotes using the style adaptive decoder or only diffusion decoder, DM means using the duration model in S\&D-LM or using a simple duration predictor of Fastspeech2, and CVQ means using the CVQ model or VQ model in the clustering style encoder.

1.Target: 我 的 背 脊 如 荒 丘 而 你 却 微 笑 摆 首 AP 把 它 当 成 整 个 宇 宙 你 与 太 阳 挥 手 也 同 海 鸥 问 候

Prompt: 直 到 那 一 天 SP 你 的 衣 衫 破 旧 而 歌 声 却 温 柔 陪 我 漫 无 目 的 的 四 处 漂 流

Successfully synthesizing the timbre, articulation method, pronunciation, pitch transition style, and rhythm.

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/prompt/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style="text-align: center">Gronud Truth</th>
			<th style="text-align: center">TCSinger</th>
			<th style="text-align: center">w/o SAD</th>
			<th style="text-align: center">w/o DM</th>
			<th style="text-align: center">w/o CVQ</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/gt/001.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/trans/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/sad/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/dm/001.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/se/001.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2.Target: 把 一 个 人 的 温 暖 转 移 到 另 一 个 的 胸 膛 AP 让 上 次 犯 的 错 反 省 出 梦 想 AP 每 个 人 都 是 这 样

Prompt: 才 能 知 道 伤 感 是 爱 的 遗 产 AP 流 浪 过 几 张 双 人 床 换 过 几 次 信 仰 才 让 戒 指 义 无 反 顾 的 交 换 AP

Successfully synthesizing the timbre, articulation method, pronunciation, pitch transition style, and rhythm.

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style="text-align: center">Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/prompt/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style="text-align: center">Gronud Truth</th>
			<th style="text-align: center">TCSinger</th>
			<th style="text-align: center">w/o SAD</th>
			<th style="text-align: center">w/o DM</th>
			<th style="text-align: center">w/o CVQ</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/gt/002.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/trans/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/sad/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/dm/002.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/abl/se/002.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

---

# Clustering Style Encoder

In these tests, we utilized the timbre of singer A and the style information of singer B to synthesize results that match the timbre of singer A while differing from that of singer B.This outcome evidentially shows that our clustering style encoder successfully decouples timbre and style in the mel spectrogram. 

1.Target: 我 们 这 些 努 力 不 简 单 快 乐 炼 成 泪 水 是 一 种 勇 敢

Successfully synthesizing the timbre of singer A, the pronunciation, pitch transition style, and rhythm of singer B.

<table style='width: 60%;'>
	<thead>
		<tr>
			<th style="text-align: center">Singer A</th>
			<th style="text-align: center">Singer B</th>
			<th style="text-align: center">Result</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/se/demo1/rt.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/se/demo1/rs.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/se/demo1/re.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

2.Target: 这 瞬 眼 的 光 景 最 亲 密 的 距 离 沿 着 你 皮 肤 纹 理

Successfully synthesizing the timbre of singer A, the pronunciation, pitch transition style, and rhythm of singer B.

<table style='width: 60%;'>
	<thead>
		<tr>
			<th style="text-align: center">Singer A</th>
			<th style="text-align: center">Singer B</th>
			<th style="text-align: center">Result</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/se/demo2/rt.wav" type="audio/wav"></audio></td>
      			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/se/demo2/rs.wav" type="audio/wav"></audio></td>
				<td style="text-align: center"><audio controls style="width: 150px;"><source src="wavs/se/demo2/re.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

---
