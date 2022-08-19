# webpage design to Control robot 
-can modification

-Designed to support smartphones




![image](https://user-images.githubusercontent.com/107868423/181578862-433c9092-555f-47f3-8f2c-d9cf010da032.png)




# web serial api





let isConnectted = false;
let port;
let writer;
var target_id;
const enc = new TextEncoder();

async function onChangespeech() {
  if (!isConnectted) {
    alert("you must connect to the usb in order to use this.");
    return;
  }
 
  try {
    const commandlist = content;
    const commandSplit = commandlist.split(" ")
    const command = commandSplit.slice(-1);
    const computerText = `${command}@`;
    await writer.write(enc.encode(computerText));
  } catch (e) {
    console.log(e);
  }
}



async function onConnectUsb() {
try {
  const requestOptions = {
    // Filter on devices with the Arduino USB vendor ID.
    filters: [{ usbVendorId: 0x2341 }],
  };

  // Request an Arduino from the user.
  port = await navigator.serial.requestPort(requestOptions);
  await port.open({ baudRate: 115200 });
  writer = port.writable.getWriter();
  isConnectted = true;
} catch (e) {
  console.log("err", e);
}
}

