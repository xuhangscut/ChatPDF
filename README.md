- 本项目支持多种文件格式，包括PDF、docx、markdown、txt等
- 本项目支持多种model，基于mindnlp支持，请查阅[mindnlp源项目](https://github.com/mindspore-lab/mindnlp)确认支持情况
- 本项目优化了RAG准确率
  - Chinese chunk切分优化，适配中英文混合文档
  - embedding优化，使用text2vec的sentence embedding，支持sentence embedding/字面相似度匹配算法
  - 检索匹配优化，引入jieba分词的rank_BM25，提升对query关键词的字面匹配，使用字面相似度+sentence embedding向量相似度加权获取corpus候选集
  - 新增reranker模块，对字面+语义检索的候选集进行rerank排序，减少候选集，并提升候选命中准确率，用`rerank_model_name_or_path`参数设置rerank模型
  - 新增候选chunk扩展上下文功能，用`num_expand_context_chunk`参数设置命中的候选chunk扩展上下文窗口大小
  - RAG底模优化，可以使用200k的基于RAG微调的LLM模型，支持自定义RAG模型，用`generate_model_name_or_path`参数设置底模
- 本项目基于gradio开发了RAG对话页面，支持流式对话

## 使用说明

#### 安装依赖

在终端中输入下面的命令，然后回车即可。
```shell
pip install -r requirements.txt
```


如果下载慢，建议配置豆瓣源或清华源。

#### 本地调用

请使用下面的命令。取决于你的系统，你可能需要用python或者python3命令。请确保你已经安装了Python。
```shell
python chatpdf.py --gen_model_type llama --gen_model_name 01-ai/Yi-6B-Chat --corpus_files sample.pdf
```
```shell
python chatpdf.py --gen_model_type qwen --gen_model_name Qwen/CodeQwen1.5-7B-Chat --corpus_files sample.pdf
```
#### 启动Web服务

```shell
python webui.py --gen_model_type llama --gen_model_name 01-ai/Yi-6B-Chat --corpus_files sample.pdf --share
```

```shell
python webui.py --gen_model_type qwen --gen_model_name Qwen/CodeQwen1.5-7B-Chat --corpus_files sample.pdf
```
如果一切顺利，现在，你应该已经可以在浏览器地址栏中输入 http://localhost:9999 查看并使用 ChatPDF 了。