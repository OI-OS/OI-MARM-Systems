# OI OS Integration Guide for OI-MARM-Systems

## ⚠️ **CURRENT STATUS: INCOMPATIBLE**

**This server cannot be installed in OI OS at this time due to incompatibility issues.**

---

## 🚨 Installation Issues

### Issue 1: Python Version Requirement

- **Required:** Python 3.10 or higher
- **System has:** Python 3.9.6 (or lower)
- **Impact:** Dependencies cannot be installed (`fastapi-mcp` requires Python 3.10+)

### Issue 2: Transport Protocol Mismatch

- **Server Type:** HTTP/WebSocket server (FastAPI-based)
- **OI OS Uses:** STDIO transport
- **Impact:** Direct connection via `brain-trust4 connect` is not possible

### Issue 3: Architecture Mismatch

- **Server runs as:** HTTP server on port 8001
- **MCP endpoint:** `http://localhost:8001/mcp`
- **WebSocket endpoint:** `ws://localhost:8001/mcp/ws`
- **Not designed for:** STDIO transport

---

## 📋 Server Information

### What is OI-MARM-Systems?

**MARM (Memory Accurate Response Mode)** is a universal MCP server providing intelligent memory that saves across sessions for AI conversations with:

- **Semantic Search** - Find memories by meaning, not keywords
- **Cross-App Memory** - Share memories between AI clients (Claude, Qwen, Gemini)
- **Auto-Classification** - Content automatically categorized for intelligent recall
- **Session Management** - Organize conversations with structured logging

### Available Tools (18 Total)

| Category | Tools |
|----------|-------|
| **Session** | `marm_start`, `marm_refresh` |
| **Memory** | `marm_smart_recall`, `marm_contextual_log` |
| **Logging** | `marm_log_session`, `marm_log_entry`, `marm_log_show`, `marm_log_delete` |
| **Notebook** | `marm_notebook_add`, `marm_notebook_use`, `marm_notebook_show`, `marm_notebook_status`, `marm_notebook_clear`, `marm_notebook_delete` |
| **Workflow** | `marm_summary`, `marm_context_bridge` |
| **System** | `marm_current_context`, `marm_system_info`, `marm_reload_docs` |

### Version

- **Current Version:** 2.2.6
- **Repository:** https://github.com/OI-OS/OI-MARM-Systems
- **Original Repository:** https://github.com/Lyellr88/MARM-Systems

---

## 🔧 Workarounds (If Needed)

### Option 1: Upgrade Python (If Possible)

If you can upgrade to Python 3.10+:

```bash
# Install Python 3.10+ and use it
python3.10 -m pip install -r requirements.txt
python3.10 server.py
```

**Note:** This still won't solve the transport mismatch issue.

### Option 2: Use Docker (Recommended for Testing)

```bash
# Pull and run the Docker container
docker pull lyellr88/marm-mcp-server:latest
docker run -d --name marm-mcp-server -p 8001:8001 \
  -v ~/.marm:/home/marm/.marm \
  lyellr88/marm-mcp-server:latest
```

**Note:** This runs the HTTP server, but OI OS cannot connect via HTTP transport.

### Option 3: Wait for HTTP Transport Support

If OI OS adds HTTP transport support in the future, this server could be connected via:
```
http://localhost:8001/mcp
```

---

## 📝 What Would Be Needed for Full Integration

### Prerequisites

1. **Python 3.10+** installed on the system
2. **HTTP Transport Support** in OI OS (currently only STDIO is supported)
3. **Dependencies installed:**
   ```bash
   pip install fastapi>=0.117.1
   pip install fastapi-mcp>=0.4.0
   pip install uvicorn>=0.36.0
   pip install sentence-transformers>=5.1.0
   # ... and other dependencies from requirements.txt
   ```

### Integration Steps (When Compatible)

1. **Install dependencies:**
   ```bash
   cd MCP-servers/OI-MARM-Systems/marm-mcp-server
   pip install -r requirements.txt
   ```

2. **Connect server (if HTTP transport is supported):**
   ```bash
   # This would require HTTP transport support in OI OS
   ./brain-trust4 connect OI-MARM-Systems http -- "http://localhost:8001/mcp"
   ```

3. **Create intent mappings** (18 tools total)
4. **Create parameter rules** for all tools
5. **Add parameter extractors** to `parameter_extractors.toml.default`

---

## 🐛 Known Limitations

### Current Limitations

1. **Cannot install** - Python version incompatibility
2. **Cannot connect** - Transport protocol mismatch (HTTP vs STDIO)
3. **No intent mappings** - Cannot be created until server is connected
4. **No parameter rules** - Cannot be created until server is connected
5. **No parameter extractors** - Cannot be created until server is connected

### Future Compatibility

This server may become compatible if:
- OI OS adds HTTP/WebSocket transport support
- Python 3.10+ becomes available on the system
- Server adds STDIO transport support (unlikely, as it's designed for HTTP)

---

## 📚 Documentation

### Official Documentation

- **MCP Handbook:** `MCP-HANDBOOK.md` - Complete usage guide with all 18 tools
- **MARM Handbook:** `MARM-HANDBOOK.md` - Original MARM protocol handbook
- **Protocol:** `PROTOCOL.md` - Quick start commands and protocol reference
- **Installation Guides:**
  - `docs/INSTALL-DOCKER.md` - Docker deployment
  - `docs/INSTALL-LINUX.md` - Linux installation
  - `docs/INSTALL-WINDOWS.md` - Windows installation

### External Resources

- **GitHub Repository:** https://github.com/OI-OS/OI-MARM-Systems
- **Original Repository:** https://github.com/Lyellr88/MARM-Systems
- **MCP Protocol:** https://modelcontextprotocol.org
- **MARM Systems:** https://marmsystems.com

---

## ✅ Verification

**Current Status:** ❌ **NOT INSTALLABLE**

To verify when compatibility is achieved:

```bash
# Check Python version
python3 --version  # Should be 3.10+

# Check if HTTP transport is supported
./brain-trust4 help connect  # Should show HTTP transport option

# Test connection (when compatible)
./brain-trust4 connect OI-MARM-Systems http -- "http://localhost:8001/mcp"
```

---

## 🎯 Summary

**OI-MARM-Systems is currently incompatible with OI OS due to:**

1. ❌ Python version requirement (3.10+ needed, system has 3.9.6)
2. ❌ Transport protocol mismatch (HTTP/WebSocket vs STDIO)
3. ❌ Architecture mismatch (HTTP server vs STDIO process)

**This server cannot be installed or configured until:**
- Python 3.10+ is available, AND
- OI OS supports HTTP transport, OR
- Server adds STDIO transport support

**Recommendation:** Use Docker for testing MARM functionality, but note that OI OS integration is not possible at this time.

---

## 📝 Installation Notes

See `INSTALLATION_NOTES.md` for detailed technical information about the incompatibility issues.

