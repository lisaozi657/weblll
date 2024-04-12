package main

import (
	"context"
	"fmt"
	"github.com/filecoin-project/lotus/api"
	"github.com/filecoin-project/lotus/chain/types"
	"github.com/filecoin-project/lotus/lib/auth"
	"github.com/filecoin-project/lotus/node/repo"
	"github.com/filecoin-project/lotus/node/repo/imports"
	"os"
)

func main() {
	ctx := context.Background()

	// 创建 Filecoin 节点的存储库
	r, err := repo.NewFS("/path/to/your/lotus/repo")
	if err != nil {
		fmt.Println("Error creating repo:", err)
		os.Exit(1)
	}

	// 打开或初始化存储库
	if err := imports.MigrateKey(r, ""); err != nil && err != repo.ErrRepoExists {
		fmt.Println("Error migrating key:", err)
		os.Exit(1)
	}

	// 加载存储库
	lr, err := r.Lock(repo.FullNode)
	if err != nil {
		fmt.Println("Error locking repo:", err)
		os.Exit(1)
	}
	defer lr.Close()

	// 创建 Filecoin API
	api, closer, err := lcli.GetFullNodeAPI(ctx, lr)
	if err != nil {
		fmt.Println("Error creating API:", err)
		os.Exit(1)
	}
	defer closer()

	// 从文件加载数据
	data, err := ioutil.ReadFile("/path/to/your/file")
	if err != nil {
		fmt.Println("Error reading file:", err)
		os.Exit(1)
	}

	// 提交存储交易
	msgCid, err := api.ClientImport(ctx, types.FileRef{Path: "/path/to/your/file"})
	if err != nil {
		fmt.Println("Error importing file:", err)
		os.Exit(1)
	}

	fmt.Println("Storage transaction submitted, message CID:", msgCid)
}
