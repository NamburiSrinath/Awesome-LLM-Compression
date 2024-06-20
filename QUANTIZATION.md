# Awesome-LLM-Quantization

<div align='center'>
  <img src=https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg >
  <img src=https://img.shields.io/github/stars/pprp/Awesome-LLM-Quantization.svg?style=social >
  <img src=https://img.shields.io/github/watchers/pprp/Awesome-LLM-Quantization.svg?style=social >
  <img src=https://img.shields.io/badge/Release-v0.1-brightgreen.svg >
  <img src=https://img.shields.io/badge/License-GPLv3.0-turquoise.svg >
 </div>

Welcome to the Awesome-LLM-Quantization repository! This is a curated list of resources related to quantization techniques for Large Language Models (LLMs). Quantization is a crucial step in deploying LLMs on resource-constrained devices, such as mobile phones or edge devices, by reducing the model's size and computational requirements.

## Papers

| Title & Author & Link                                        | Introduction                                                 | Summary                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ICLR22 <br>[GPTQ: Accurate Post-Training Quantization for Generative Pre-trained Transformers](https://arxiv.org/abs/2210.17323) <br> Elias Frantar, Saleh Ashkboos, Torsten Hoefler, Dan Alistarh <br> [Github](https://github.com/IST-DASLab/gptq) | ![image-20240529203728325](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240529203728325.png) | This Paper is the first one to apply post-training quantization to GPT. GPTQ is a one-shot weight quantization method based on approximate second-order information(Hessian). The bit-width is reduced to 3-4 bits per weight. Extreme experiments on 2-bit and ternary quantization are also provided. <br />#PTQ #3-bit #4-bit #2-bit |
| ICML23<br>[SmoothQuant: Accurate and Efficient Post-Training Quantization for Large Language Models](https://arxiv.org/abs/2211.10438) <br> Guangxuan Xiao, Ji Lin, Mickael Seznec, Hao Wu, Julien Demouth, **Song Han** <br> [Github](https://github.com/mit-han-lab/smoothquant) | ![image-20240529213948826](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240529213948826.png) | SmoothQuant is a post-training quantization framework targeting W8A8 (INT8). In General, weights are easier to quantize than activation. It propose to migrate the quantization difficulty from activations to weights using mathematically equivalent transformation using $`s = \frac{\left( \max \left( \lvert X \rvert \right) \right)^\alpha}{\left( \max \left( \lvert W \rvert \right) \right)^{1-\alpha}}`$.<br />#PTQ #W8A8 #Outlier |
| MLSys24_BestPaper <br> [AWQ: Activation-aware Weight Quantization for LLM Compression and Acceleration](https://arxiv.org/abs/2306.00978) <br>Ji Lin, Jiaming Tang, Haotian Tang, Shang Yang, Wei-Ming Chen, Wei-Chen Wang, Guangxuan Xiao, Xingyu Dang, Chuang Gan, Song Han, **Song Han** <br> [Github](https://github.com/mit-han-lab/llm-awq) | ![image-20240529214839469](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240529214839469.png) | Activation-aware Weight Quantization (AWQ) is low-bit weight-only quantization method targeting edge devices with W4A16. The motivation is protecting only 1% of sliant weighs can retain the performance. Then, AWQ aims to search for the optimal per-channel scaling $`s^* = \arg\min_{s} \left\Vert Q \left( W \cdot \text{diag}(s) \right) \left( \text{diag}(s)^{-1} \cdot X \right) - W X \right\Vert`$ to protect the salient weights by observing the activation. Then, we have $Q(w\cdot s)\cdot \frac{x}{s}$.<br />#PTQ #W4A16 #Outlier |
| AAAI24 Oral <br /> [OWQ: Outlier-Aware Quantization for Efficient Fine-tuning and Inference of Large Language Models](https://arxiv.org/abs/2306.02272) <br /> Changhun Lee, Jungyu Jin, Taesu Kim, Hyungjun Kim, Eunhyeok Park <br /> [Github]([xvyaward/owq: Code for the AAAI 2024 Oral paper "OWQ: Outlier-Aware Weight Quantization for Efficient Fine-Tuning and Inference of Large Language Models". (github.com)](https://github.com/xvyaward/owq)) | ![image-20240608223236808](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240608223236808.png) | Outlier-aware weight quantization (OWQ) aims to minimize the footprint through low-precision representation. It prioritizes a small subset of structured weight using Hessain matrices and applies the high precision to these subset. This approach is a mixed-precision quantization method. The final model is 3.1 bit, which achieves comparable performance to OPTQ in 4-bit. Moreover, it incorporates Weak Column Tuning using PEFT to further boost the quality of zero-shot tasks.  <br />#PTQ #Mixed-Precision #3-bit #PEFT |
| EMNLP23 <br /> [Outlier Suppression+: Accurate quantization of large language models by equivalent and optimal shifting and scaling](https://arxiv.org/abs/2304.09145) <br />Xiuying Wei, Yunchen Zhang, Yuhang Li, Xiangguo Zhang, Ruihao Gong, Jinyang Guo, Xianglong Liu <br /> [Github](https://github.com/ModelTC/Outlier_Suppression_Plus) | ![image-20240605160952404](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240605160952404.png) | In PTQ of LLM, outliers are constrated in specific channels and are asymmetric across channels. To address it, Outlier Suppression+ (OS+), a PTQ framework, is proposed with channel-wise shifting for asymmetry and channel-wise scaling for concentration. Also, they propose a fast and stable scheme to calculate the hyperparameters within the shifting and scaling. (1) Channel-wise Shifting can reshape the asysmetric shapes to symmetric distribution (2) Channel-wise Scaling scales down the outliers to a threshold, resulting a unified range for different channels. (3) Unified Migration Pattern can make sure the equivalent to the original results. <br /> #PTQ #Outlier |
| ACL24 Long Paper<br />[BitDistiller: Unleashing the Potential of Sub 4-bit LLMs via Self-Distillation](http://arxiv.org/abs/2402.10631)<br />Dayou Du, Yijia Zhang, Shijie Cao, Jiaqi Guo, Ting Cao, Xiaowen Chu, Ningyi Xu<br />[Github](https://github.com/DD-DuDa/BitDistiller) | ![image-20240603211630312](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240603211630312.png) | Bitdistiller is a QAT framework that utilizes Knowledge Distillation to boost the performance at Sub-4bit. BitDistiller (1) incorporates a tailored asymmetric quantization and clipping technique to perserve the fidelity of quantized weight and (2) proposes a Confidence-Aware Kullback-Leibler Divergence (CAKLD) as self-distillation loss. Experiments involve 3-bit and 2-bit configuration. <br />#QAT #2-bit #3-bit #KD |
| ICML24 <br>[BiLLM: Pushing the Limit of Post-Training Quantization for LLMs](https://arxiv.org/abs/2402.04291) <br> Wei Huang, Yangdong Liu, Haotong Qin, Ying Li, Shiming Zhang, Xianglong Liu, Michele Magno, Xiaojuan Qi <br> [Github](https://github.com/Aaronhuang-778/BiLLM) | ![image-20240529225417121](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240529225417121.png) | BiLLM is the first 1-bit post-training quatization framework for pretrained LLMs. BiLLM split the weights into salient weight and non-salient one. For the salient weights, they propose the binary residual approximation strategy. For the unsalient weights, they propose an optimal splitting search to group and binarize them independently. BiLLM achieve 8.41 ppl on LLaMA2-70B with only 1.08 bit.<br />#PTQ #1-bit |
| Arxiv23 <br /> [BitNet: Scaling 1-bit Transformers for Large Language Models](https://arxiv.org/abs/2310.11453) <br /> Hongyu Wang, Shuming Ma, Li Dong, Shaohan Huang, Huaijie Wang, Lingxiao Ma, Fan Yang, Ruiping Wang, Yi Wu, Furu Wei <br /> [Github](https://github.com/kyegomez/BitNet) | ![image-20240609193123523](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240609193123523.png) | BitNet focus on QAT for 1-bit LLMs. It employs low-precision binary weights and quantized 8-bit activations, while maintaining high precision for the optimizer states and gradients during training. BitLinear is proposed as plug-and-play module that replace all linear modules in Transformer. For training, (1) It employs STE to approximate the gradient. (2) It maintains a latent weight in a high-precision format to accumulate the paramter update. (3) It employs large learning rate to avoid the biased gradient. <br />#QAT #1-bit |
| ACL24 <br /> [DB-LLM: Accurate Dual-Binarization for Efficient LLMs](https://arxiv.org/pdf/2402.11960) Hong Chen, Chengtao Lv, Liang Ding, Haotong Qin, Xiabin Zhou, Yifu Ding, Xuebo Liu, Min Zhang, Jinyang Guo, Xianglong Liu, Dacheng Tao | ![image-20240610171838682](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240610171838682.png) | DB-LLM introduces Flexible Dual Binarization (FDB) by splitting 2-bit quantized weights into two independent set of binaries (which is similar to BiLLM). It also proposes Deviation -Aware Distillation to focus differently on various samples. DB-LLM is actually a QAT framework that targeting W2A16 settings.  <br />#QAT #Binarization #2-bit |
| Arxiv24 <br>[SliM-LLM: Salience-Driven Mixed-Precision Quantization for Large Language Models](https://arxiv.org/abs/2405.14917) <br> Wei Huang, Haotong Qin, Yangdong Liu, Yawei Li, Xianglong Liu, Luca Benini, Michele Magno, Xiaojuan Qi <br> [Github](https://github.com/Aaronhuang-778/SliM-LLM) | ![image-20240529231050896](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240529231050896.png) | This paper presents Slience-Driven Mixed-Precision Quantization for LLMs, called Slim-LLM, targeting 2-bit mixed precision quantization. Specifically, Silm-LLM involves two techniques: (1) Salience-Determined Bit Allocation (SBA): by minimizing the KL divergence between original output and the quantized output, the objective is to find the best bit assignment for each group. (2) Salience-Weighted Quantizer Calibration: by considering the element-wise salience within the group, Slim-LLM search for the calibration parameter $\gamma$ to prevent the degradation of local salient weight information in each group.<br />#MixedPrecision #2-bit |
| Arxiv24<br>[AdpQ:A Zero-shot Calibration Free Adaptive Post Training Quantization Method for LLMs](https://arxiv.org/abs/2405.13358v1) | ![image-20240603205727796](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240603205727796.png) | This paper formulates outlier weight identification problem in PTQ as the concept of shinkage in statistical ML. By applying Adaptive LASSO regression model, AdpQ ensures the quantized weights distirbution is close to that of origin, thus eliminating the requirement of calibration data. Lasso Regression employ the L1 regularization and minimize the KL divergence between the original weight and quantized one. The experiments mainly focus on 3/4 bit quantization<br />#PTQ #Regression |
| Arxiv24<br /> [Integer Scale: A Free Lunch for Faster Fine-grained Quantization for LLMs](https://arxiv.org/abs/2405.14597v2) <br /> Qingyuan Li, Ran Meng, Yiduo Li, Bo Zhang, Yifan Lu, Yerui Sun, Lin Ma, Yuchen Xie | ![image-20240603212845404](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240603212845404.png) | Integer Scale is a PTQ framework that require no extra calibration and maintain the performance. It is a fine-grained quantization method and can be used plug-and-play. Specifically, it reorder the sequence of costly type conversion I32toF32. <br />#PTQ #W4A16 #W4A8 |
| Arxiv24<br />[QuaRot: Outlier-Free 4-Bit Inference in Rotated LLMs](https://arxiv.org/abs/2404.00456)<br />Saleh Ashkboos, Amirkeivan Mohtashami, Maximilian L. Croci, Bo Li, Martin Jaggi, Dan Alistarh, Torsten Hoefler, James Hensman<br />[Github](https://github.com/spcl/QuaRot) | ![image-20240603215015646](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240603215015646.png) | This paper introduce a novel rotation-based quantization scheme, which can quantize the weight, activation, and KV cache of LLMs in 4-bit. QuaRot rotates the LLMs to remove the outliers from hideenstate. It apply randomized Hadamard transformations to the weight matrices without changing the model. When applying this transformation to attention module, it enables the KV cache quantization. <br />#PTQ #4bit #Rotation |
| Arxiv24<br />[SpinQuant:LLM Quantization with Learned Rotations](https://arxiv.org/abs/2405.16406v2)<br />Zechun Liu, Changsheng Zhao etc. | ![image-20240603214042270](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240603214042270.png) | Rotating activation or weight matrices heps remove outliers and benefits quantizaion (rotational invariance property). They first identify a collection of applicable rotation parameterizations that lead to identical outputs in full-precision Transformer. They find that soem **random rotations lead to better quantization** than others. Then, SpinQuant was proposed to optimize the rotation matrices with _Cayley_ optimization on validation dataset. Specifically, them employ Cayley SGD method to optimize the rotation matrix on the Stiefel manifold. <br />#PTQ #Rotation #4bit |
| NeurIPS2024 <br /> [Outliers and Calibration Sets have Dimishing Effect on Quantization of Mordern LLMs](https://arxiv.org/abs/2405.20835v1)<br /> Davide Paglieri, Saurabh Dash, Tim Rocktaschel, Jack Parker-Holder | ![image-20240604110208446](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240604110208446.png) | This paper evaluates the effects of calibration set on the performance of LLM quantization, especially on hidden activations. Calibration set can distort the quantization range and negatively impact performance. This paper reveals that different model has shown different tendency towards quantization. (1) OPT has shown high susceptibility to outliers with varying calibration sets. (2) Newer models like Llama-2-7B, Llama-3-8B, Mistral-7B has demonstrated stronger robustness. This findings suggest a shift in PTQ strategies. These findings indicate that we should emphasis more on optimizing inference speed rather than focusing on outlier preservation. <br />#Analysis #Evaluation #Finding |
| Arxiv24<br /> [Effective Interplay between Sparsity and Quantization: From Theory to Practice]()<br /> Simla Burcu Harma Ayan Chakraborty, Elizaveta Kostenok, Dnila Mishin, etc. <br /> [Github](https://github.com/parsa-epfl/quantization-sparsity-interplay) | ![image-20240604125632861](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240604125632861.png) | This paper dives into the interplay between sparsity and quantization and evaluates whether thheir combination impacts final performance of LLMs. This paper theriotically proves that applying sparsity before quantization is the optimal sequence, minimizing the error in computation. The experiments involves OPT, LLaMA and ViT. Findings: (1) sparsity and quantization are not orthogonal; (2) interaction between Sparsity and quantization significantly harm the performance, where quantization error is playing a dominant role in the degradation. <br />#Theory #Sparisty |
| NeurIPS23<br /> [QLoRA: Efficient Finetuning of Quantized LLMs](https://arxiv.org/abs/2305.14314)<br /> Tim Dettmers, Artidoro Pagnoni, Ari Holtzman, Luke Zettlemoyer <br /> [Github](https://github.com/artidoro/qlora) | ![image-20240604191811055](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240604191811055.png) | QLoRA aims to reduce the memory usage of LLM by incoorporating the LoRA with 4-bit quantized pretrained model. Specifically, QLoRA introduces (1) 4-bit NormalFlot(NF4), a information theoretically optimal for normally distributed weights. (2) double quantization to reduce the memory footprint. (3) paged optimizers to manage memory spikes. <br />#NF4 #4-bit #LoRA |
| NeurIPS23<br />[QuIP: 2-Bit Quantization of Large Language Models with Guarantees](https://proceedings.neurips.cc/paper_files/paper/2023/file/0df38cd13520747e1e64e5b123a78ef8-Paper-Conference.pdf) <br />Jerry Chee, Yaohui Cai, Volodymyr Kuleshov, Christopher De Sa <br /> [Github](https://github.com/Cornell-RelaxML/QuIP) |                                                              | This paper introduces Quantization with Incoherence Processing (QuIP), which is based on the insight that quantization benefits from incoherent weight and Hessian matrices. It consists of two steps (1) adaptive rounding procedure to minimize a quadratic proxy objective. (2) pre- and post-processing that ensures weight and Hessian incoherence using random orthgonal matrices. QuIP makes the two-bit LLM compression viable for the first time. <br />#PTQ #2-bit #Rotation |
| ICML24 <br /> [AQLM: Extreme Compression of Large Language Models via Additive Quantization](https://arxiv.org/pdf/2401.06118v2) <br /> [Github](https://github.com/vahe1994/AQLM) | ![image-20240610123542382](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240610123542382.png) |                                                              |
| Arxiv24 <br /> [PV-Tuning: Beyond Straight-Through Estimation for Extreme LLM Compression](https://arxiv.org/pdf/2405.14852) <br />  [Github](https://github.com/vahe1994/AQLM) | ![image-20240610125319660](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240610125319660.png) |                                                              |
| EMNLP23 <br /> [LLM-FP4: 4-Bit Floating-Point Quantized Transformers](https://arxiv.org/abs/2310.16836) <br />Shih-yang Liu, Zechun Liu, Xijie Huang, Pingcheng Dong, Kwang-Ting Cheng <br /> [Github](https://github.com/nbasyl/LLM-FP4) | ![image-20240609211009863](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240609211009863.png) | LLM-FP4 quantizes both weight and activation to FP4 in  a post-training manner. Compared with INT quantization, FP quantization is more flexible and can better handle long-tail or bell-shaped distributions. FP quantization is sensitive to the exponent bits and clipping range. LLM-FP4 searches for the optimal quantization parameters. This paper observes a pattern, which is high inter-channel variance and low intra-channel variance. Thus, LLM-FP4 employ per-channel activation quantization. <br />#PTQ #FP4 |
| ICLR24 Spotlight<br /> [OmniQuant: Omnidirectionally Calibrated Quantization for Large Language Models](https://arxiv.org/pdf/2308.13137) <br /> Wenqi Shao, Mengzhao Chen, Zhaoyang Zhang, Peng Xu, Lirui Zhao, Zhiqian Li, Kaipeng Zhang, Peng Gao, Yu Qiao, Ping Luo <br /> [Github](https://github.com/OpenGVLab/OmniQuant) | ![image-20240605153427027](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240605153427027.png) | This paper is a framework between PTQ and QAT, aiming to attain the performance of QAT and maintain the time and data efficiency of PTQ. OmniQuant just requires 1.6h for LLaMA-7B, while LLM-QAT requires 90h and SmoothQuant requires 10min. Specifically, OmniQuant freezes the original full-precision weight and only train a few learnable quantization parameters, including Learnable Weight Clipping (LWC) and Learnable Equivalent Transformation (LET). <br /> #PTQ #QAT #Learnable #Transformation |
| Arxiv23 <br /> [LLM-QAT: Data-Free Quantization Aware Training for Large Langugae Models](https://arxiv.org/abs/2305.17888) <br /> Zechun Liu, Barlas Oguz, Changsheng Zhao, Ernie Chang, Pierre Stock, Yashar Mehdad, Yangyang Shi, Raghuraman Krishnamoorthi, Vikas Chandra | ![image-20240609215624544](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240609215624544.png) | LLM-QAT is a data-free distillation method that leverages generations produced by the pre-trained model (also teacher model). Besides quantizing the weights and activations, LLM-QAT also quantize the KV cache, which helps to increase the throughput and support long sequence. The experiments are conducted on 4-bits. Experiments are conducted on a single 8-GPU training node. <br />#QAT #KVQuant #KD |
| Arxiv23 <br /> [PB-LLM: Partially Binarized Large Language Models](https://arxiv.org/abs/2310.00034) <br /> Yuzhang Shang, Zhihang Yuan, Qiang Wu, Zhen Dong <br /> [Github](https://github.com/hahnyuan/PB-LLM) | ![image-20240609212807570](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240609212807570.png) | PB-LLM is a mixed-precision quantization framework that filters a small ratio of salient weights to higher-bit. It analyzed the performance under PTQ and QAT settings. Under PTQ, it reconstruct the binarized weight matrix like GPTQ. Under QAT, it freezes the salient weights during training. <br />#PTQ #QAT #1-bit |
| Arxiv24<br /> [I-LLM: Efficient Integer-Only Inference for Fully-Quantized Low-Bit Large Language Models](https://arxiv.org/abs/2405.17849) <br /> Xing Hu, Yuan Chen, Dawei Yang, Zhihang Yuan, Jiangyong Yu, Chen Xu, Sifan Zhou | ![image-20240610110609330](https://github.com/pprp/Awesome-LLM-Quantization/blob/main/asset/image-20240610110609330.png) | I-LLM is a PTQ framework that targeting the Integer-only quantization. They identify the large fluctuation of activations across channels and tokens. (1) It develop Fully-Smooth Block-Reconstruction (FSBR) to aggressively smooth inter-channel variations of all activations and weights. (2) It proposes Dynamic Integer-only MatMul (DI-MatMul) to dynamically quantize the input and output with int-only operations. (3) It proposes a series of bit shift to execute non-linear operation, including DI-ClippedSoftmax, DI-Exp, DI-Normalization. <br />#PTQ #Int-Only #W4A4 |

## Perplexity Evaluation

2-bit evaluation

![](./asset/quantization_2bit.png)

3-bit evaluation

![](./asset/quantization_3bit.png)

## Contributing

Contributions to this repository are welcome! If you have any suggestions for new resources, or if you find any broken links or outdated information, please open an issue or submit a pull request.

## License

This repository is licensed under the [MIT License](https://opensource.org/licenses/MIT).