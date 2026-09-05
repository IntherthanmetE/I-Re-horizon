# K2 Horizon — Layer Map

## Layer 0

10 tensors, all in model-00001-of-00048.safetensors

- input_layernorm.weight — [2560]
- self_attn.q_proj.weight — [4096, 2560]
- self_attn.k_proj.weight — [1024, 2560]
- self_attn.v_proj.weight — [1024, 2560]
- self_attn.o_proj.weight — [2560, 4096]
- self_attn.gate_proj.weight — [4096, 2560]
- post_attention_layernorm.weight — [2560]
- mlp.gate_proj.weight — [6144, 2560]
- mlp.up_proj.weight — [6144, 2560]
- mlp.down_proj.weight — [2560, 6144]

Layer 0 is dense.

## Layer 3

377 tensors, all in model-00004-of-00048.safetensors

- LayerNorm: 2
- MoE experts: 300
- MoE router: 2
- Shared expert: 3
- Attention: 4
- MoVA V-experts: 64
- MoVA router: 2

MoE:
- 100 experts
- 8 experts/token
- 3 tensors/expert

MoVA:
- 64 V-experts
- 4 V-experts/token
- V-router shape [64, 2560]

## Confirmed Remote Range Reading

Safetensors HTTP Range reading works with HTTP 206.

Layer 3 V-router:
- shape [64, 2560]
- dtype BF16
- bytes: 327680

Layer 3 V-router bias:
- shape [64]
- dtype BF16
- bytes: 128

Embedding:
- shape [250624, 2560]
- dtype BF16
- row size: 5120 bytes

Tested token embeddings:
- token 35789
- token 34163

Layer 0 input RMSNorm:
- shape [2560]
- dtype BF16
- bytes: 5120

Layer 0 attention weights:
- Q [4096, 2560]
- K [1024, 2560]
- V [1024, 2560]
- O [2560, 4096]
- gate [4096, 2560]

## Important

Weights are NOT stored in this repository.
Only metadata, source code, analysis and future scripts are stored here.
