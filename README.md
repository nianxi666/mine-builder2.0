🏗️ Mine Builder 2.0<div align="center">AI-Powered Text-to-Minecraft Building Generator  Transform your imagination into Minecraft structures with multimodal AI🎮 Live Demo • 📚 Documentation • 🚀 Quick Start • 🎯 Examples</div>✨ FEATURES / 核心功能🎨 TEXT TO IMAGE / 文本到图像 — Nano Banana model generates 518×518 images from text prompts in ~1.8s.    模型从文本提示生成 518×518 图像，耗时约 1.8 秒。🧱 IMAGE TO 3D / 图像到 3D — Hierarchical 3D generation with 8192-dim latent space and DINOv2 ViT-g/14 encoder.    使用分层生成与 8192 维潜空间（DINOv2 ViT-g/14）生成精细 3D 网格。🎭 AI MATERIALS / AI 自动选材 — Gemini 2.5 Flash vision-language model assigns Minecraft block materials (≈92.3% accuracy).    使用 Gemini 2.5 Flash 为部件智能匹配 Minecraft 方块材料。🔄 REAL-TIME PREVIEW / 实时预览 — Interactive Three.js viewer with part-level editing and multi-view rendering.    可交互 3D 预览，支持部件级编辑与多视图渲染。📦 SCHEMATIC EXPORT / 蓝图导出 — Convert directly to Minecraft 1.12 .schematic (NBT + GZIP).    直接导出为 .schematic 文件，兼容 Minecraft 1.12。💾 SAVE/LOAD SYSTEM / 保存与加载 — Persistent state with localStorage + ZIP export for session recovery.    支持本地保存、ZIP 导出与会话恢复。🎮 Live Demo / 在线演示Try it now: 👉 https://pumpkinai.space/Mine-builderAlternative Demo: 👉 https://nianxi666.github.io/mine-builder-demo🖼️ Live Demo Screenshot（已添加仓库截图）Example Outputs / 示例展示<div align="center">Fantasy CastleModern BuildingTree House<img src="001.jpeg" width="250" alt="Fantasy Castle" /><img src="1.png" width="250" alt="Modern Building" /><img src="final_ai_artwork.png" width="250" alt="Tree House" />Prompt: medieval fortress with towersPrompt: minimalist glass structurePrompt: organic forest dwelling</div>🏗️ System Architecture / 系统架构 (概览)┌────────────────────┐
│  Text Input        │
│  "A castle..."     │
└─────────┬──────────┘
          │
          ▼
┌─────────────────────┐
│  Nano Banana (T2I)  │  ⚡ ~1.8s
│  518×518 image      │
└─────────┬───────────┘
          ▼
┌──────────────────────────┐
│  3D Generation Model     │  🧠 Dual Volume Packing
│  • Flow: 8192-dim latent │  DINOv2 ViT-g/14
│  • VAE: 384³ resolution  │  Part-aware decoding
└─────────┬────────────────┘
          ▼
┌──────────────────────────┐
│  Gemini 2.5 Flash        │  🎨 Material Intelligence
│  • Global style analysis │  Context-aware selection
│  • Part-level reasoning  │  92.3% accuracy
└─────────┬────────────────┘
          ▼
┌──────────────────────────┐
│  Voxelization (32³)      │  📦 NBT Encoding
│  + Schematic Export      │  GZIP compression
└──────────────────────────┘
🚀 Quick Start / 快速开始PrerequisitesPython 3.10+CUDA-capable GPU (recommended: RTX 4090 with 24GB VRAM)16GB+ RAMGemini API Key — Get one hereInstallation# Clone the repo
git clone [https://github.com/nianxi666/mine-builder2.0.git](https://github.com/nianxi666/mine-builder2.0.git)
cd mine-builder2.0

# Optionally checkout feature branch
git checkout feat/persist-materials-localstorage

# Install Python dependencies
pip install -r requirements.txt

# (Optional) Save your Gemini API key
echo "YOUR_GEMINI_API_KEY" > key.txt
Run the AppOption 1 — Interactive Web Interfacepython server.py
# Open http://localhost:5000
Option 2 — Gradio (Image→3D only)python app.py
# Open http://localhost:7860
Option 3 — CLI: Convert voxel TXT to .schematicpython txt_to_schematic.py voxel_output.txt my_building.schematic
📖 Usage Guide / 使用说明1️⃣ Generate from TextStart server: python server.pyEnter Gemini API key when promptedUpload reference image (or use text-only)Click Run AI Agent to auto-generate materials & voxelizationExport .schematic and import into Minecraft2️⃣ Manual EditingSelect parts in the 3D viewer to apply materialsDelete voxels or paint on voxel gridCamera: orbit / zoom / reset with UI buttons3️⃣ AdvancedMulti-view collage to help material assignmentSave full session (ZIP) including voxel data + chat historyLoad previous saves from file or URL🔧 Configuration / 配置Model / app parameters (edit app.py)LATENT_SIZE = 4096      # Per-part latent dimension (total: 8192)
HIDDEN_DIM = 1536
GRID_RES = 384
FLOW_SHIFT = 3.0
LOGITNORM_MEAN = 1.0
LOGITNORM_STD = 1.0
Server options (server.py)# Start with pre-loaded model
python server.py --input_model path/to/model.glb

# Start with saved session
python server.py --input_data path/to/save.zip

# Custom port
python server.py --port 8080
📊 Technical Specifications / 技术规格Parameter               Value             Notes                           Latent Dimension       4096 × 2         Dual-part latent               Visual Encoder         DINOv2 ViT-g/14   Feature extraction             Hidden Dimension       1536             Internal size                   VAE Decoding Resolution384³             High-fidelity internal         Output (Minecraft)     32³               Voxel output for game           End-to-End Time         ~14.7s (RTX 4090)T2I + I23D + materials + encodeMaterial Accuracy       92.3%             Measured on test set           Part Recognition       96.7%             -                               Compressed File Size   ~8.4KB           Typical schematic (compressed) 🎨 Supported Minecraft BlocksSupports 150+ Minecraft 1.12 vanilla blocks, e.g.:Building: Stone, Cobblestone, Stone Brick, Oak/Spruce/etc planksDecorative: Wool (16), Concrete (16), Stained Glass (16), Terracotta (16)Natural: Grass, Dirt, Sand, Leaves, LogsFunctional: Stairs, Slabs, Fences, Doors, Redstone components<details><summary>Click to expand full block categories</summary>Building Blocks: Stone, Cobblestone, Stone Brick, Smooth Stone, Oak/Spruce/Birch/Jungle/Acacia/Dark Oak Planks, Bricks, Nether Brick, End Stone BrickDecorative Blocks: Wool (all 16 colors), Concrete (all 16 colors), Stained Glass (all 16 colors), Terracotta (all 16 colors)Natural Blocks: Grass, Dirt, Sand, Gravel, Leaves, Logs (all wood types), Water, Lava, IceFunctional Blocks: Stairs, Slabs, Fences (all materials), Doors, Trapdoors, Pressure Plates, Redstone components</details>📂 Project Structuremine-builder2.0/
├── server.py              # Main Flask app with 3D viewer
├── app.py                 # Gradio interface for image-to-3D
├── txt_to_schematic.py    # Voxel-to-schematic converter
├── requirements.txt       # Python dependencies
├── key.txt                # (Optional) Gemini API key storage
├── input/                 # Input models & reference images
├── cache/                 # Downloaded model cache
├── saves/                 # Exported sessions
├── assets/                # Images, icons, demo assets
├── data/                  # Training data & configs
├── flow/                  # Flow model implementation
├── vae/                   # VAE model implementation
└── docker/                # Docker configs
🐛 Troubleshooting / 常见问题API Key Invalid# Ensure key is correct and not expired:
# [https://aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
Out of Memory (OOM)# reduce voxel resolution
VOXEL_RESOLUTION = 16
Model Download FailsCheck console for model URLs and manually download from Hugging Face if needed.Texture Pack Not Loadingtexture_pack.zip
  └── assets/minecraft/textures/blocks/*.png
🤝 ContributingWe welcome contributions!Fork the repoCreate a feature branch: git checkout -b feature/your-featureCommit & push: git commit -m "Add feature" / git push origin feature/your-featureOpen a Pull RequestGuidelinesFollow PEP 8 for PythonAdd docstrings & unit testsUpdate docs for new features📄 LicenseImportant: This project is for NON-COMMERCIAL USE ONLY.🙏 AcknowledgmentsBase: Forked from NVlabs/PartPackerDiffusion: Nano BananaVision-Language: Google Gemini 2.5 FlashFeature Extraction: DINOv2 by Meta AITexture Pack: Faithful 32xRendering: Three.jsBackground removal: rembg📚 Citation@software{mine_builder_2025,
  title = {Mine Builder 2.0: AI-Powered Text-to-Minecraft Building Generator},
  author = {nianxi666},
  year = {2025},
  url = {[https://github.com/nianxi666/mine-builder2.0](https://github.com/nianxi666/mine-builder2.0)},
  note = {Multimodal generation system for Minecraft schematic files}
}
🗺️ RoadmapShort-term (v2.1)[ ] 64³ / 128³ voxel support[ ] Batch generation[ ] Style transfer from reference images[ ] Enhanced text-based editingLong-term (v3.0)[ ] End-to-end text → voxel model[ ] Physical stability simulation[ ] Redstone circuit generation[ ] Support for Terraria, Roblox, 
