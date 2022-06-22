# dero-pong-server

### Generating Build Scripts

There is a helper script `run_secret_server` in the `bin` folder

It takes 3 positional arguments: discord_url, price_in_units, and purchase_banner (optional)

example:

```bash
bin/run_secret_server "https://discord.gg/SXTzd7YPUU" 4 "Purchase Secret Discord Server Invite URL"
```

or just

```bash
bin/run_secret_server "https://discord.gg/SXTzd7YPUU" 4
```

`run_secret_server` will take the given arguments and create a new file tagged with the current date and time under the `run` folder:

`run/secret_server_%YYYY-%MM-%DD_%H%M%S.go`

### How-to Make a DERO Pong_Server

**secretnamebasis**

Preliminary Information

These instructables were mobile optimized for Android. If that's a drag that they were made for Android and not linux, hit me up and I would be happy to build the instructions for linux (they are like the same). I am certain that you could 'think' your way through these instructions to do it on mac and windows - but that's not my territory.

These instructables need you to compile DERO packages from source because you will be altering source code. There are changes that you are going to be making to DERO's source code to make it optimized for your use-case. This example assumes a fresh install of Termux (at minimum cleared storage and cache).

These instructions are a literal step-by-step walk through. I use lots of pictures, and they are big because they are mobile images. Some people might not like that, but I won't know unless you comment below ;)  

Also, you CANNOT use --fastsync in this example or your wallet won't show the transactions because you will only have the blocks, and not the individual transactions themselves. #sorrynotsorry

PROTIP: you can zoom in and zoom out with the pinching gesture, like you would a map on your phone.

PROTIP: you can 'tab-complete' by pressing the double arrows (↹) under the ESC button, this is wicked handy btw. Say you need to cd into something long like rpc_examples, when you type rp and then touch the Tab button (↹), it auto fills in the rest.

PROTIP: when you see someone type `cd ..` the `..` sends you further up the file pipe line

PROTIP: `ctrl`+`w` means you hit the `ctrl` button and then `w`

## Obtain the necessary prerequisites

Gather your Android device with a minimum of 64 gigs of space. Better on 128 gigs, but 32 gigs is a no go. The phone will fill up with the entire blockchain and lock up. (obligatory: no iphones)

Install and open Termux: https://f-droid.org/repo/com.termux_118.apk

![image](https://user-images.githubusercontent.com/86203717/174068906-716e2f22-f6d4-4c59-b88c-d8f49d781ca4.png)
![image](https://user-images.githubusercontent.com/86203717/174068965-9374a892-5808-4b97-b213-3f4ffeaa18a6.png)

```termux-change-repo```

![image](https://user-images.githubusercontent.com/86203717/174068991-dbf8aa6d-f88e-467e-92c5-cb27c5fe8806.png)


touch the `Ok` button

![image](https://user-images.githubusercontent.com/86203717/174069042-5d1f52b6-d0e7-4add-ab54-f9a44e34a050.png)


select the Grimler mirror by touching it and then hit 'Ok'

![image](https://user-images.githubusercontent.com/86203717/174069158-dcec8f22-f19c-44a3-8412-ddbf91ca5fa6.png)

![image](https://user-images.githubusercontent.com/86203717/174069213-b5764ace-58e2-4aa1-bd6b-e89b600d0a13.png)


`pkg install git golang wget rsync`

![image](https://user-images.githubusercontent.com/86203717/174069244-4e8c0854-4af7-40de-b1ed-c52646d7cb29.png)

you will be asked if you want to download these packages, type in `y` and press enter

![image](https://user-images.githubusercontent.com/86203717/174069314-32c59712-45d1-4bf2-9444-a63262222808.png)

you will be asked if you want to update openssl, type `y` and then press enter

![image](https://user-images.githubusercontent.com/86203717/174069433-93fd8e5e-0be6-4a7f-85cb-fd60bb07437b.png)

`pkg update`

![image](https://user-images.githubusercontent.com/86203717/174069453-92f16771-a1a7-4d8b-bfdd-8be219a0ba40.png)

 you will be asked if you want to update termux-tools, type `y` and press enter again

![image](https://user-images.githubusercontent.com/86203717/174069624-d13edabb-df1f-40ac-b376-f46f633968e7.png)

you will be asked if you want to update motd, type `y` and press enter

![image](https://user-images.githubusercontent.com/86203717/174069704-4f952f2d-d81e-4985-a6ba-c1086acc2eed.png)

you will be asked if you want to update motd-playstore, type `y` and press enter

![image](https://user-images.githubusercontent.com/86203717/174069724-aa8daf8f-aebd-4847-9853-9fdfadd18117.png)

you will be asked if you want to update sources.list, type `y` again and then press enter

![image](https://user-images.githubusercontent.com/86203717/174069752-6dd7a5c4-2308-4cd6-a220-635e7d8aa40f.png)

`mkdir dero-linux`

![image](https://user-images.githubusercontent.com/86203717/174069807-fff23ec1-76ae-4454-a501-4ef10b576233.png)

`ls`

![image](https://user-images.githubusercontent.com/86203717/174069916-67f13dee-8019-45b9-a9e5-5f83a3218947.png)

`git clone https://github.com/deroproject/derohe`

![image](https://user-images.githubusercontent.com/86203717/174069988-23e4b8cf-3b18-4779-a1c2-308bc4d1f57f.png)

You will now have two files in termux, to see type in `ls` and press enter

![image](https://user-images.githubusercontent.com/86203717/174070017-3f7857ad-7d0f-46c2-9b37-6b3e109d46e1.png)

## Play with DERO-HE Source Code

The whole goal here is that we are going to construct our pong_server in the derohe file, and then we are going to compile it into and use it from dero-linux,

Now you can take the fast route to the next part, or you can take the scenic route by looking at the directories and files along the way (recommended if you are interested in exploring more of derohe)

### Scenic route

`cd derohe`

`ls`

`cd cmd`

`ls`

`rpc_examples`

`ls`

`cd pong_server`

### Fast route  

`cd /derohe/cmd/rpc_examples/pong_server/`

![image](https://user-images.githubusercontent.com/86203717/174070335-1c562100-edf2-40d1-8c04-93b42bc17eb3.png)

`ls`

![image](https://user-images.githubusercontent.com/86203717/174070368-ef230106-0729-4aa2-8e58-3a4dc3779cf8.png)

You will see that there is a file called pong_server.goand dummy_test.go

We need to remove the pong_server.go file and replace it with one that Capt made that I have as a repo

`rm pong_server.go`

![image](https://user-images.githubusercontent.com/86203717/174070431-306bf49e-1cfb-4aa0-9dc3-55444174bf58.png)

`ls`

![image](https://user-images.githubusercontent.com/86203717/174070495-9ebb2084-83a8-44a4-add1-3474bd9be840.png)

You can see that the pong_server.go package is now gone. So now let's replace it with the pong_server I was given by CaptianDERO

`wget https://github.com/secretnamebasis/dero-pong-server/releases/download/release1/pong_server.go`

![image](https://user-images.githubusercontent.com/86203717/174070555-0fc44185-bde5-4608-ad45-1bc96893d93f.png)

`ls`

![image](https://user-images.githubusercontent.com/86203717/174070584-29d95a42-4996-496c-8a25-b1cc93bdd1f2.png)

And there it is, the pong_server.go file I got from @CaptainDero

We are going to edit this pong_server.go file to something a little more to our use-case. And for this example, we are going to be making pong_server that TX Replies a private discord server url when people pay 0.01 DERO

There are a few things that we need to change: the `RPC_COMMENT` that tells them what they are buying at point of sale, `RPC_VALUE_TRANSFER` that sets how much they need to send to trigger the pong to their ping,  the `RPC_COMMENT` that delivers the information to their list of transactions and `fmt.Sprintf(message)` that echoes that `RPC_COMMENT`

A note here, you can alter the code using any text editor. But for the simplicity of the users, I chose `nano` over `vim`. My personal preference is `vim`, but I am not going to teach people how to use something so powerful when I already in the middle of doing that.

`nano pong_server.go`

![Screenshot_20220616-064405](https://user-images.githubusercontent.com/86203717/174072299-7fde8300-887f-4a97-ab15-2b794efcbaa2.png)

Search for the point-of-sale `RPC_COMMENT` by using the `ctrl`+`w`

Type `Purchase PONG` in the search

![Screenshot_20220616-065038](https://user-images.githubusercontent.com/86203717/174073500-34b88970-6cd8-4994-a195-974dd62ddcd2.png)

press enter

![Screenshot_20220616-064957](https://user-images.githubusercontent.com/86203717/174073543-aa186474-1a21-4873-b992-23fb3aa3b23d.png)


Change `PONG` to `Secret Discord Server Invite URL`

![Screenshot_20220616-065305](https://user-images.githubusercontent.com/86203717/174073812-deefaf9a-89a0-4cd8-b129-e4ec085c985d.png)

Now lets set the price of the `pong_server` by searching again with `ctrl`+`w`

`Value: uint64(2)}`

![Screenshot_20220616-065610](https://user-images.githubusercontent.com/86203717/174074508-ae01db89-3529-43fa-bfcb-dfcef2522298.png)

Press enter

![Screenshot_20220616-065601](https://user-images.githubusercontent.com/86203717/174074535-fbd15a7a-821e-4d25-9707-b559984de4ac.png)


This is how much you want them to send to get the TX Reply, in atomic units. So that means that right now it is set to 0.00002. Ww want it to be 0.001 and in atomic units thats 100 (let's keep it 100, ya'll)

Change `2` to `100`

![Screenshot_20220616-065905](https://user-images.githubusercontent.com/86203717/174074994-f0ee5c82-ba98-42b1-80ca-4ba1934d9a86.png)

Now let's change the deployable that they will be getting in their list of transactions. That's what the TX Reply does, it replies to transactions after all, and so you would find the information in your list of transactions.

`ctrl`+`w`

`Successfully`

Press `enter`

![Screenshot_20220616-070330](https://user-images.githubusercontent.com/86203717/174075710-a839a0fd-8c6d-41a3-9477-7ca16cf87bd3.png)

Change `pong (this could be serial/license key or download link or further)`

to `Secret Discord Server Invite URL: https://discord.gg/2PZZp9hh`

or what ever you want to send in their list of transactions; respecting of course the 128 character count limit.

![Screenshot_20220616-071340](https://user-images.githubusercontent.com/86203717/174077579-1a5a7f7b-92fa-48c4-ad23-aa93361e6099.png)


Now let's echo this change further downstream for the user

`ctrl`+`w`

`Sucessfully`, Yes, it has a typo, which makes it easier to find

Press `enter`

![Screenshot_20220616-071445](https://user-images.githubusercontent.com/86203717/174077885-5dab3a23-2691-4ffb-adce-0a224b669565.png)

change `pong (could be serial, license or download link or anything).`

to `Secret Discord Server Invite URL: https://discord.gg/2PZZp9hh .`

![Screenshot_20220616-071805](https://user-images.githubusercontent.com/86203717/174078723-11ebec92-6e1b-45f7-a53d-f8702c6cddd4.png)

now save the file `ctrl`+`x`

It is going to ask you if you want to `Save modified buffer?`

![Screenshot_20220616-072245](https://user-images.githubusercontent.com/86203717/174079428-ade7c034-e22c-47f0-b87d-11ae615e343a.png)

`y`

And then press `enter` when it says `File Name to Write: pong_server.go`

![Screenshot_20220616-072305](https://user-images.githubusercontent.com/86203717/174079591-982c8a9d-7e38-40fe-b844-4bf48dfca56b.png)

## Compile DERO-HE to run in Linux environment

Now we are going to compile the code and to do that, we need to leave our pong_server directory and go back up the folder tree to derohe.

`cd ~/derohe`

![Screenshot_20220616-072842](https://user-images.githubusercontent.com/86203717/174080535-4ba18b79-0f27-4358-b468-0ccd18bfbef8.png)

And here is where we let `go` build our edits into executable files and drop the outputs into our dero-linux file. All we have to do is...

`go build -o ~/dero-linux/ ./...`

Now if it hangs for a minute, that's okay. Some devices compile the code fater than others. And as Captian says, 'Have faith in your machine'

![Screenshot_20220616-073212](https://user-images.githubusercontent.com/86203717/174081233-5e06ab1c-083d-44c6-ab83-8dd91f39a96b.png)

Let's go look in on our exectuables

`cd ~/dero-linux`

`ls`

![Screenshot_20220616-073415](https://user-images.githubusercontent.com/86203717/174081794-4b81d8ae-544f-4313-9b2b-d055f7689d5f.png)

Congrats! You have compiled from source code you have changed! Now, Execute!

## Executing dero executables

Now we need a copy of mainnet, but in addition to all the blocks we also need our mainnet folder to have all the transactions. So you have two choices: slow (and decentralized), fast (and centralized)

The slow and decentralized way to get synced with mainnet in to run `./derod`

For this example we used the fast and centralized way to get synced with mainnet is to collect a copy of `mainnet` from seed node. To do this we use

`rsync --inplace --port=2048 -a rsync://141.95.86.80/DEROblockchainDB/mainnet ./`

![Screenshot_20220616-080059](https://user-images.githubusercontent.com/86203717/174087205-f26f99f4-2fa6-435d-a3a7-9200edfae551.png)

As you can see, this hangs. And it takes roughly 45 mins. Once this is done syncing with network, it will drop to the pipeline or errors will happen. Most likely storage error.

Then you will execute the DERO daemon

`./derod`

![Screenshot_20220616-104506_Termux](https://user-images.githubusercontent.com/86203717/174125573-274103b0-9298-468c-b2f8-6f94dc0bb8ae.jpg)

open a few new terminal sessions by pulling the drawer from the left hand screen

![Screenshot_20220616-125731_Termux](https://user-images.githubusercontent.com/86203717/174146973-97f39912-bb2e-419f-84a6-b286e6de6cc2.jpg)


`./dero-wallet-cli --rpc-server`

open, rebuild from seed or make a wallet named `rpc` wallet (2min-2hrs)


![Screenshot_20220616-125303_Termux](https://user-images.githubusercontent.com/86203717/174146682-7d96dd6d-280f-4763-af97-f7c099af1fe0.jpg)


Pull open the drawer of sessions from the left hand edge and start the `pong_server`. It will likely begin dumping errors at you, that's normal.

`./pong_server`

![Screenshot_20220616-125535_Termux](https://user-images.githubusercontent.com/86203717/174147675-6a520c87-661d-406a-82f9-317be624cfe2.jpg)


Now hit `ctrl`+`c`to kill the process and look at the two Integrated Addresses.

The first is `(without hardcoded amount)` you don't collect this one.

You need to collect the second one because it has the hardcoded amount

![Screenshot_20220616-125654_Termux](https://user-images.githubusercontent.com/86203717/174147644-b1620abc-7a95-44fe-91f1-781e601a9945.jpg)

## Testing the pong_server

open a new terminal session

`./dero-wallet-cli`

open, rebuild from seed or make a new wallet and register hot-wallet (2mins-2hrs)

![Screenshot_20220616-125758_Termux](https://user-images.githubusercontent.com/86203717/174148356-c31a96e1-bbb3-4fc8-97e2-f0fd38dd57bc.jpg)

select transfer dero with option `5` and paste integrated address, the one that *isn't* `(without harcoded amount)`

![Screenshot_20220616-125841_Termux](https://user-images.githubusercontent.com/86203717/174148419-e2ff0624-7a8c-412f-bb48-092acf917e0d.jpg)

hit `y` to send to the address with the amount listed

![Screenshot_20220616-125851_Termux](https://user-images.githubusercontent.com/86203717/174148568-2def5b9c-76ea-4c1e-9393-4b47bc832dad.jpg)

And the transaction is in to the network and takes to the count of...

`1,2,3,4,5,6,7,8,9,10,12,13,14,15,16,17,18`

And if you are quick, you can pull open the drawer to the `pong_server` and watch the transaction get processed

![Screenshot_20220616-125913_Termux](https://user-images.githubusercontent.com/86203717/174148739-e0af44fc-4af1-481d-b955-6853570fc451.jpg)

Now open the drawer and jump over to the session with your hot-wallet running and select `13` to see the wallet transaction history.

![Screenshot_20220616-125955_Termux](https://user-images.githubusercontent.com/86203717/174148903-d24c2077-88ba-406d-8863-3ee037063253.jpg)

you should see that there is, buried in all the code, the invite code to the Secret Discord Server

![Screenshot_20220616-132622_Termux](https://user-images.githubusercontent.com/86203717/174149488-8d309b75-aaaa-4c86-a5a2-a9e97926b5c1.jpg)

Now copy and paste the link url into your browser and see for your self that it works.

![Screenshot_20220616-130045_Firefox](https://user-images.githubusercontent.com/86203717/174149649-cfe1f2b3-ed85-48ed-a108-6eb836a7015c.jpg)

SUCCESS! You have made your first PONG_SERVER!

Now take a moment to think about what this means. You can create your own paywall for nearly anything you want in a private, encrypted and trustless way.

Go forth and share the power of DERO!
