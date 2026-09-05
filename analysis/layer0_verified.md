# Layer 0 Verified Checkpoint

All 10 Layer 0 tensors were successfully read via HTTP Range requests
from model-00001-of-00048.safetensors.

Header size: 1360
Data base: 1368

## Tensor map

1. input_layernorm.weight
   shape: [2560]
   offset: [0, 5120]

2. mlp.down_proj.weight
   shape: [2560, 6144]
   offset: [5120, 31462400]

3. mlp.gate_proj.weight
   shape: [6144, 2560]
   offset: [31462400, 62919680]

4. mlp.up_proj.weight
   shape: [6144, 2560]
   offset: [62919680, 94376960]

5. post_attention_layernorm.weight
   shape: [2560]
   offset: [94376960, 94382080]

6. self_attn.gate_proj.weight
   shape: [4096, 2560]
   offset: [94382080, 115353600]

7. self_attn.k_proj.weight
   shape: [1024, 2560]
   offset: [115353600, 120596480]

8. self_attn.o_proj.weight
   shape: [2560, 4096]
   offset: [120596480, 141568000]

9. self_attn.q_proj.weight
   shape: [4096, 2560]
   offset: [141568000, 162539520]

10. self_attn.v_proj.weight
    shape: [1024, 2560]
    offset: [162539520, 167782400]

## Verified statistics

### input_layernorm.weight
min: 0.15527344
max: 2.25
mean: 0.51087606
std: 0.32667086

### post_attention_layernorm.weight
min: 0.0024719238
max: 0.80078125
mean: 0.23321232
std: 0.040031955

### mlp.down_proj.weight
shape: [2560, 6144]
min: -1.71875
max: 1.96875
mean: 1.0230336e-05
std: 0.024303593

### mlp.gate_proj.weight
shape: [6144, 2560]
min: -0.6328125
max: 1.7265625
mean: -6.1136576e-05
std: 0.021840433

### mlp.up_proj.weight
shape: [6144, 2560]
min: -0.30273438
max: 0.26953125
mean: 1.8759056e-06
std: 0.020529686

### self_attn.gate_proj.weight
shape: [4096, 2560]
min: -0.29101562
max: 0.46289062
mean: 0.0002564055
std: 0.023187201

### self_attn.k_proj.weight
shape: [1024, 2560]
min: -0.3515625
max: 0.3515625
mean: -2.433297e-05
std: 0.023381673

### self_attn.o_proj.weight
shape: [2560, 4096]
min: -1.3671875
max: 1.46875
mean: -1.0755333e-06
std: 0.022258991

### self_attn.q_proj.weight
shape: [4096, 2560]
min: -0.31445312
max: 0.28515625
mean: 5.3761596e-06
std: 0.019602422

### self_attn.v_proj.weight
shape: [1024, 2560]
min: -0.23828125
max: 0.27929688
mean: 2.6900301e-05
std: 0.023798214

## Verification

All 10/10 Layer 0 tensors have been successfully read.
All Range requests returned HTTP 206.
All observed byte lengths and tensor shapes match the safetensors index.

Weights were read directly from Hugging Face without downloading the full model.
