# Reaching the keeper from a Mac that runs FLEx in Parallels

The keeper's phase-2 bridge listens **only on the loopback address inside the Windows VM**
(`127.0.0.1:<port>`). It is meant for the Researcher Panel in a browser, and a browser will only
talk plain HTTP to `localhost`: an HTTPS page such as the panel cannot fetch `http://10.211.55.15`,
because that is mixed content. So the browser must always see the keeper as `localhost`, and on a
Mac host that means one Parallels port-forwarding rule. (VirtualBox, QEMU and other hypervisors have
the same feature; if you run one of those you already know where it is.)

## One-time setup in Parallels Desktop

1. The VM must use **Shared Network** (the default). Check under the VM's *Configure…* ▸ Hardware ▸
   Network ▸ Source.
2. Open **Parallels Desktop ▸ Preferences** (called *Settings* on recent macOS), then the
   **Network** tab.
3. Under *Shared network*, find the **Port forwarding rules** list and click **+**.
4. Fill in the rule:
   - **Protocol:** TCP
   - **Source port:** the keeper's port (shown on the keeper's Setup screen; default 47811)
   - **Forward to:** pick your Windows VM by name (or type its address, e.g. 10.211.55.15)
   - **Destination port:** the same port
5. Click **OK**, then **OK** again to close Preferences. No VM restart is needed.

## Check it

With the keeper running in the VM, open `http://localhost:47811/ping` in the Mac's browser (use the
port you chose). The keeper answers with its name and version. The keeper's Setup screen has a
*Test from this browser* button that does the same call and explains the result.

If it does not answer: confirm the keeper is running in the VM and shows the same port; confirm the
rule's *Forward to* names the VM that is actually running; confirm the VM is on Shared Network.
Parallels applies the rule to connections arriving at the Mac, its own loopback included; if a
Parallels version turns out not to forward loopback, the fallback is an SSH tunnel
(`ssh -L 47811:127.0.0.1:47811 <user>@<vm-address>`), which the keeper's installer can set up.

## What the rule does and does not expose

The rule only reaches the keeper's port, and the keeper still enforces its own checks: only the
panel's origins are allowed (CORS with a required custom header, so every call is preflighted), a
pairing token the panel shows once is required on every call, and the Host header must be
`localhost` or `127.0.0.1` with the expected port. Chrome's private-network preflight is answered
with `Access-Control-Allow-Private-Network: true`.

Sources: Parallels KB 124718 "Port forwarding in Parallels Desktop"; Parallels Desktop User's Guide,
Network Preferences and Shared Network Settings.
