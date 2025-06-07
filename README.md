 

# 输入：chatgpt_export.json 文件（已上传）
# 输出：格式化 txt 文本字符串

import json

def handle_upload(file):
    # 读取文件内容
    raw_data = file.read()
    data = json.loads(raw_data)

    # 可选：提取 conversation 标题或其他元数据
    messages = data.get("messages", [])

    formatted_lines = []

    for msg in messages:
        role = msg.get("role", "")
        content = msg.get("content", "").strip()
        
        if not content:
            continue

        if role == "user":
            formatted_lines.append(f"梅宝：{content}")
        elif role == "assistant":
            formatted_lines.append(f"阿景：{content}")
        else:
            formatted_lines.append(f"{role}：{content}")

    # 拼接成完整文本
    result_text = "\n\n".join(formatted_lines)

    return {"formatted_txt": result_text}