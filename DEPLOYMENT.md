# No-LLM daily arXiv digest

This fork ranks new arXiv papers against Zotero items with abstracts and emails the
original abstracts. It does not need an OpenAI or other model API key.

The checked-in `config/custom.yaml` selects `cs.CR`, `cs.LG`, and `cs.AI`, uses the
local embedding reranker, and sends through `smtp.163.com:465`. The scheduled
workflow runs at 22:00 UTC (06:00 Asia/Shanghai).

In the repository's **Settings → Secrets and variables → Actions**, set these
repository secrets:

| Secret | Value |
| --- | --- |
| `ZOTERO_ID` | Numeric Zotero account user ID |
| `ZOTERO_KEY` | Zotero web API key with read access to the relevant library |
| `SENDER` | 163 Mail sender address |
| `RECEIVER` | Address that receives the digest |
| `SENDER_PASSWORD` | 163 Mail SMTP authorization code, not the account login password |

Sync Zotero Desktop with the Zotero account and ensure some journal articles,
conference papers, or preprints contain abstracts. The local Zotero API setting
alone does not sync the library to Zotero's web API.

Run the **Test** workflow manually under Actions to check the pipeline and
delivery. The scheduled **Send emails daily** workflow skips email when there
are no new papers. Do not put credentials in `config/custom.yaml`, repository
variables, or a public commit.
