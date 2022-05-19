## admin

### admin.peers
  + Lấy ra thông tin về những node kết nối trong cùng mạng
    ```
      > admin.peers
      [{
          caps: ["eth/66", "snap/1"],
          enode: "enode://f2f3845ea755331ea5fe94a36f5a4e7b3e6573e8a82afe48cf491dd469b33595fd46898b772284a27cbf6b4a34264fbc7b6b329836d30b637bb374c625cee25a@127.0.0.1:30305",
          id: "0d83313282f41687f804015a7ad980dbb3d3cd0820ccae1d08500e4ac3ef6693",
          name: "Geth/v1.10.18-unstable-eb69f490/linux-amd64/go1.18",
          network: {
            inbound: false,
            localAddress: "127.0.0.1:33178",            // địa chỉ của node hiện tại
            remoteAddress: "127.0.0.1:30305",           // địa chỉ của node kết nối đến 
            static: true,
            trusted: false
          },
          protocols: {
            eth: {
              difficulty: 444,
              head: "0x4d8cf8b0ad672944a23acdf898d0c05724950efb92c239eda333dd291f206f29",
              version: 66
            },
            snap: {
              version: 1
            }
          }
      }]
    ```