---
layout: page
title: Dog vs Cat 
description: A simple image classifier using fast.ai 
img: assets/img/Nashoba.jpg
importance: 1
category: Deep Learning
---

<input id="photo" type="file">
<div id="results"></div>

<iframe
    src="https://nessmaykerchen-catvsdogclassifier.hf.space/"
    frameborder="0"
    width="850"
    height="450"
></iframe>

<!-- <script>
  async function loaded(reader) {
    const response = await fetch('https://hf.space/embed/nessmaykerchen/catvsdogclassifier/+/api/predict', {
      method: "POST", body: JSON.stringify({ "data": [reader.result] }),
      headers: { "Content-Type": "application/json" }
    });
    const json = await response.json();
    const label = json['data'][0]['confidences'][0]['label'];
    results.innerHTML = `<br/><img src="${reader.result}" width="300"> <p>${label}</p>`
  }
  function read() {
    const reader = new FileReader();
    reader.addEventListener('load', () => loaded(reader))
    reader.readAsDataURL(photo.files[0]);
  }
  photo.addEventListener('input', read);
</script> -->


<!-- <script>
import { client } from "@gradio/client";

<!-- 
async function run() {

	const response_0 = await fetch("https://raw.githubusercontent.com/gradio-app/gradio/main/test/test_files/bus.png");
	const exampleImage = await response_0.blob();
						
	const app = await client("https://nessmaykerchen-catvsdogclassifier.hf.space/");
	const result = await app.predict("/predict", [
				exampleImage, 	// blob in 'img' Image component
	]);

	console.log(result?.data);
}

run();
</script> --> -->