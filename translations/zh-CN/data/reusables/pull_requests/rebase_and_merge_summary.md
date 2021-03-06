在 {% data variables.product.product_location %} 上的拉取请求中选择 **Rebase and merge（变基并合并）**选项时，来自主题分支（或头部分支）的所有提交都会单独添加到基础分支，而无需合并提交。 这样，通过维护线性项目历史记录，变基和合并行为类似于[快进合并](https://git-scm.com/docs/git-merge#_fast_forward_merge)。 但是，变基可以通过使用新提交在基本分支上重写提交历史记录来实现此目的。

{% data variables.product.product_name %} 上的变基和合并行为与 `git rebase` 略有偏差。 {% data variables.product.prodname_dotcom %} 上的变基和合并始终会更新提交者信息并创建新的提交 SHA，而 {% data variables.product.prodname_dotcom %} 外部的 `git rebase` 在提交原型上发生变基时不改变提交者信息。 有关 `git rebase` 的更多信息，请参阅 Git 文档中的 [git-rebase](https://git-scm.com/docs/git-rebase)。

要变基并合并拉取请求，必须在仓库中拥有[写入权限](/articles/repository-permission-levels-for-an-organization/)，并且仓库必须[允许变基合并](/articles/configuring-commit-rebasing-for-pull-requests/)。

有关 `git rebase` 的可视表示，请参阅 _Pro Git_ 一书中的[“Git 分支 - 变基”一章](https://git-scm.com/book/en/Git-Branching-Rebasing)。
