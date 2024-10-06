<img src="icons/diago-text.png" width="300" alt="DIAGO">

[![Go Report Card](https://goreportcard.com/badge/github.com/emiago/diago)](https://goreportcard.com/report/github.com/emiago/diago)
![Coverage](https://img.shields.io/badge/coverage-61.1%25-blue)
![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/emiago/diago)

Short for **dialog + GO**.  
**A library for building communication (VOIP) solutions in GO!**

**For more information and documentation, visit [the website](https://emiago.github.io/diago)**

Quick links:
- [Getting started](https://emiago.github.io/diago/docs/getting_started/)
- [Demo Examples](https://emiago.github.io/diago/docs/examples/)
- [API Docs](https://emiago.github.io/diago/docs/api_docs/)
- [GO Docs](https://pkg.go.dev/github.com/emiago/diago)

*If you find this project useful and you want to support/sponsor or need help in your projects, you can contact me on*
[mail](mailto:emirfreelance91@gmail.com)

Follow me on [X/Twitter](https://twitter.com/emiago123) for regular updates.

## Contributions
Please open issues first instead of submitting PRs. The library is under development and may not have the latest code pushed.


## Usage 

Check out more in [Getting started](https://emiago.github.io/diago/docs/getting_started/) but for quick view, here is echotest (hello world) example.
```go 
ua, _ := sipgo.NewUA()
dg := diago.NewDiago(ua)

dg.Serve(ctx, func(inDialog *diago.DialogServerSession) {
	inDialog.Progress() // Progress -> 100 Trying
	inDialog.Answer(); // Answer

	// Make sure file below exists in work dir
	playfile, err := os.Open("demo-echotest.wav")
	if err != nil {
		fmt.Println("Failed to open file", err)
		return
	}
	defer playfile.Close()

	// Create playback and play file.
	pb, _ := inDialog.PlaybackCreate()
	if err := pb.Play(playfile, "audio/wav"); err != nil {
		fmt.Println("Playing failed", err)
	}
}
```

See more [examples in this repo](/examples)
### Tracing SIP, RTP

When opening an issue, consider enabling some traces.

```go
sip.SIPDebug = true // Enables SIP tracing
media.RTCPDebug = true // Enables RTCP tracing
media.RTPDebug = true // Enables RTP tracing. NOTE: It will dump every RTP Packet
```
