<h1>MMagic Service Compute Nest Deployment and Usage Documentation</h1>

<h2>Overview</h2>

<p>Using Compute Nest, you can deploy the MMagic environment with a single click in seconds, immediately starting your AIGC journey with MMagic. Without Compute Nest, you might spend hours or even longer on environment preparation and service deployment. Based on Compute Nest, you can significantly improve your work efficiency and focus your energy on business algorithm logic.</p>

<p>MMagic (Multimodal Advanced, Generative, and Intelligent Creation) is an open-source AIGC toolbox for professional AI researchers and machine learning engineers to process, edit, and generate images and videos. MMagic allows researchers and engineers to use state-of-the-art pre-trained models and easily train and develop new custom models.</p>

<p>MMagic supports various foundational generative models, including:</p>
<ul>
    <li>Unconditional Generative Adversarial Networks (GANs)</li>
    <li>Conditional Generative Adversarial Networks (GANs)</li>
    <li>Internal Learning</li>
    <li>Diffusion Models</li>
    <li>And many other generative models coming soon!</li>
</ul>

<p>MMagic supports various applications, including:</p>
<ul>
    <li>Text-to-Image Generation</li>
    <li>Image Translation</li>
    <li>3D Generation</li>
    <li>Image Super-Resolution</li>
    <li>Video Super-Resolution</li>
    <li>Video Frame Interpolation</li>
    <li>Image Completion (Inpainting)</li>
    <li>Image Matting</li>
    <li>Image Restoration</li>
    <li>Image Colorization</li>
    <li>Image Generation</li>
    <li>And many other applications coming soon!</li>
</ul>

<h2>Instance Description</h2>

<p>The MMagic deployment is the community open-source version. For source code, please refer to the <a href="https://github.com/open-mmlab/mmagic" target="_blank">Github Repo</a>. Currently available instance specifications are as follows:</p>

<table border="1" cellspacing="0" cellpadding="5">
    <thead>
        <tr>
            <th>Instance Family</th>
            <th>vCPU & Memory</th>
            <th>System Disk</th>
            <th>GPU/FPGA</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ecs.gn7i-c16g1.4xlarge</td>
            <td>16 vCPU 60 GiB</td>
            <td>200G</td>
            <td>1 * NVIDIA A10 (24G)</td>
        </tr>
        <tr>
            <td>ecs.gn7i-c32g1.8xlarge</td>
            <td>32 vCPU 188 GiB</td>
            <td>200G</td>
            <td>1 * NVIDIA A10 (24G)</td>
        </tr>
        <tr>
            <td>ecs.gn7i-c32g1.16xlarge</td>
            <td>64 vCPU 376 GiB</td>
            <td>200G</td>
            <td>2 * NVIDIA A10 (24G)</td>
        </tr>
        <tr>
            <td>ecs.gn7i-c32g1.32xlarge</td>
            <td>128 vCPU 752 GiB</td>
            <td>200G</td>
            <td>4 * NVIDIA A10 (24G)</td>
        </tr>
    </tbody>
</table>

<p>Estimated costs can be viewed in real-time during instance creation.</p>

<h2>Deployment Process</h2>

<h3>0. Preparation</h3>

<p>Before正式 using the service, you need an Alibaba Cloud account to access and create resources such as ECS and VPC.</p>

<ul>
    <li>If you are using a personal account, you can create service instances directly.</li>
    <li>If you are using a RAM user to create service instances, and it is your first time using Alibaba Cloud Compute Nest:
        <ul>
            <li>You need to add permissions for the corresponding resources to the RAM user account before creating the service instance. For detailed operations on adding RAM permissions, please refer to <a href="https://help.aliyun.com/document_detail/121945.html" target="_blank">Authorize RAM Users</a>. The required permissions are listed in the table below.</li>
            <li>You also need to authorize the creation of associated roles. Refer to the figure below and select <strong>Agree to Authorize and Create Associated Role</strong>.</li>
        </ul>
    </li>
</ul>

<h3>1. Deployment Entry</h3>

<p>You can search for it yourself in Alibaba Cloud Compute Nest, or quickly reach it via the deployment link below.<br>
<a href="https://computenest.console.aliyun.com/user/cn-hangzhou/serviceInstanceCreate?spm=5176.24779694.0.0.5fce4d22PjIn0o&ServiceId=service-ffad3a27316440039df3" target="_blank">Deployment Link</a></p>

<h3>2. Create Service Instance</h3>

<p>Click the creation link.<br>
Click "Confirm Order" to enter.<br>
After confirming the order information, click "Create Now".<br>
Wait until the service instance status becomes "Deployed", then click the instance ID link to enter the service instance details page.<br>
Click "Login Address" to enter the file browser.<br>
Enter the username and password set during service instance creation to log in.<br>
Subsequent results of MMagic inference examples performed on the instance can be conveniently viewed here.</p>

<h2>Instance Demonstration</h2>

<h3>Execution Environment</h3>

<p>After creating the MMagic service instance via Compute Nest, you need to enter the command line console:<br>
Click Remote Connection.<br>
Click Password-Free Login.<br>
Log in using the default session management.</p>

<pre><code>sudo su - # Switch to root
docker start mmagic
docker exec -it mmagic /bin/bash
cd data
## run the following example cases</code></pre>

<p>The data directory mentioned above can be viewed via the web service provided by the local machine. The image content output by the demonstrations below can also be viewed directly through the browser.</p>

<h3>Text-to-Image</h3>

<p>Generate images from text based on the Stable Diffusion model:</p>

<pre><code>python demo/mmagic_inference_demo.py \
        --model-name stable_diffusion \
        --text "A panda is having dinner at KFC" \
        --result-out-dir demo_text2image_stable_diffusion_res.png</code></pre>

<p><strong>ControlNet-Canny</strong></p>

<pre><code>python demo/mmagic_inference_demo.py \
        --model-name controlnet \
        --model-setting 1 \
        --text "Room with blue walls and a yellow ceiling." \
        --control 'https://user-images.githubusercontent.com/28132635/230297033-4f5c32df-365c-4cf4-8e4f-1b76a4cbb0b7.png' \
        --result-out-dir demo_text2image_controlnet_canny_res.png</code></pre>

<p><strong>ControlNet-Pose</strong></p>

<pre><code>python demo/mmagic_inference_demo.py \
        --model-name controlnet \
        --model-setting 2 \
        --text "masterpiece, best quality, sky, black hair, skirt, sailor collar, looking at viewer, short hair, building, bangs, neckerchief, long sleeves, cloudy sky, power lines, shirt, cityscape, pleated skirt, scenery, blunt bangs, city, night, black sailor collar, closed mouth" \
        --control 'https://user-images.githubusercontent.com/28132635/230380893-2eae68af-d610-4f7f-aa68-c2f22c2abf7e.png' \
        --result-out-dir demo_text2image_controlnet_pose_res.png</code></pre>

<h3>Image Translation</h3>

<pre><code>python demo/mmagic_inference_demo.py \
        --model-name pix2pix \
        --img ./resources/input/translation/gt_mask_0.png \
        --result-out-dir demo_translation_pix2pix_res.png</code></pre>

<h3>Image Super-Resolution</h3>

<pre><code>python demo/mmagic_inference_demo.py \
        --model-name esrgan \
        --img ./resources/input/restoration/0901x2.png \
        --result-out-dir demo_restoration_esrgan_res.png</code></pre>

<p>The super-resolution image information obtained after image super-resolution is as follows:</p>

<h3>More Examples</h3>

<p>For more examples, please refer to the README.md in the file browser. It also includes video processing related examples. We look forward to your deeper exploration and welcome you to practice and supplement corresponding cases to this document.</p>

<h2>References</h2>

<ol>
    <li><a href="https://mmagic.readthedocs.io/zh_CN/latest/" target="_blank">https://mmagic.readthedocs.io/zh_CN/latest/</a></li>
    <li><a href="https://zhuanlan.zhihu.com/p/624831412" target="_blank">https://zhuanlan.zhihu.com/p/624831412</a></li>
    <li><a href="https://zhuanlan.zhihu.com/p/637904586" target="_blank">https://zhuanlan.zhihu.com/p/637904586</a></li>
</ol>
