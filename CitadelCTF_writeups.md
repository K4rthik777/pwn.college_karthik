# Zahard's Welcome
The base of Citadel rises before you, its great doors sealed with fractured steel and dead circuitry.
Faded corporate protocols still hum in the lock, relics of the world that fell.

Those who came before tried to climb but all failed. Their echoes linger as fragments of voices,
reminders of broken attempts to free humanity. Now you have chosen to take their place. You will be the
one to scale the Citadel and finish what they could not.

The voices of the fallen whisper through the static: "The path begins in the gathering place. There,
candidates are chosen". Here is your invitation.

Step into the gathering place where all climbers are briefed before the ascent.

## Solve
The flag was hidden among one of the channels in the discord server.So we checked each one and found it.

Flag: ```bash citadel{7h3_c174d3l_b3ck0n5}```

# The social network
 
🗼OSINT pt1: The ascent begins. The first floor is not metal or binaries but of memory. Among the echoes, one voice lingers, of an early climber. He was among the earliest to challenge the Citadel, and though he failed, his traces remain scattered across the ruins of the old world.

It is said that the key to the next floor can be found by tracing the socials of this legendary climber. Start by checking out citadweller on Instagram.

## Solve
We just went on to instagram to find citadweller account and found the first half of the flag in the highlight and then went onto X to find the account with same username and found the second half there.

Flag: ```bash citadel{17_1s_jus7_7h3_b3g1nn1ng}```

# Omniscent Flag's Metadata
As you step into the second chamber, a figure manifests before you. Before you stands a forgotten deity, a dead god spoken of only in whispers. Known by countless names: “Apostle of Epilogue and Eternity,” “Lone Messiah” and many more lost to time.

They leave nothing but a single image, a relic carrying his final secret. Hidden within its layers lies the key to ascend to the next chamber.

## Solve
I took the image provided and put it in Cyberchef tool and used the (Extract Files) operation on it. This got me the flag image.

Flag: ```bash citadel{th1s_ch4ll3ng3_1s_f0r_th4t_0n3_ex1ft00l_4nd_b1nw4lk_enthus14st}```

# track 8
Bypassing the second chamber leads to an empty floor except for a single artifact in the center: an old MP3 player, scratched and worn. On its surface, a cipher is etched, a message left behind for anyone who can decode it:

```bash
twj eys zpr ukm 'viamnwqw' bx lzgo: esmqqui{yyr_oshwwcm_bwupa}
```
When you power it on, the sound fills the chamber. The tracks play like whispers from a lost world, and you recognize it as a song from Panchiko’s latest studio album, particularly track no. 8. Its title feels familiar, hinting at a famous cipher. Decrypt it by using the album name as your key and continue your ascent.

## Solve
We used an online Vigenere Decoder to decode given text with the key as album name ginkgo to get another key panchiko to decode the new cipher to get the flag.  

Flag: ```bash citadel{add_vinegar_twice} ```

# Test of Sweetness
This floor feels like a digital world. The space is an illusion, all pink and sweet, stretching around you in impossible patterns. Here, you are no longer a climber but just another user.

Ahead, a door glows faintly. It is the only path forward and requires a level of authority you do not yet have. Fragments of session memory flicker, hinting at what it might take to gain higher access.

## Solve
 We changed the user status to admin by changing the value of user in the cache cookies and got the flag.

Flag: ```bash citadel{fru1tc4k3_4nd_c00k13s}  ```

# Rotten Apple
Among the debris of this floor, you find a relic of sound: An album which turns out to be D>E>A>T>H>M>E>T>A>L by Panchiko, a long lost album. But the music is warped, as though it has undergone disc rot.

The path forward is hidden in the distortion. Similar to how the album was warped, the password to the next floor has been warped first by a factor of 47, then by a factor of 13. Untangle these changes to reveal the code and continue your ascent.

## Solve
We used the (ROT13) and (ROT47) operation seperately until we got to the flag.

Flag: ```bash  citadel{b3tt3r_ROTt3n} ```

# Randomly Accessed Memories

On your ascent to this floor, you hear these fragments being played back —

```bash
clone it, pull it, reset it, stage it, 
commit, push it, fork, rebase it. 
merge it, branch it, tag it, log it, 
add it, stash it, diff, untrack it … 
```

You look around and discover a chamber containing a vast archive of Daft Punk’s music, intertwined with cryptic commits left behind by other musicians. They seem ordinary at first glance, but not everything in the history is what it seems. The archive:
 https://github.com/evilcryptonite/daft-punk-archive

## Solve 
we went through the commit history for some clues and while doing that we found the third chunk and then found second and first chunks in this order. Correctly aligning them according to numbering, we decoded them using (From Base64) operation in Cyberchef.

Flag: ```bash citadel{w3_4r3_up_4ll_n1t3_t0_g1t_lucky} ```

# Selected Ambient Work
The symphonic adventure does not end here. On the next floor, a single song keeps echoing through the floor, repeating in a haunting loop. Amid the sound, you find a note left by a past candidate. It hints that the song holds a secret message, hidden in plain sight, much like how Aphex Twin concealed his face within his music with the help of spectrograms.

To move forward, you must find the message hidden in this sound.

Note: Separate the words in the flag with _ and make it UPPERCASE. Example: citadel{S3L3CT3D_AMB13NT_W0RK}

## Solve
We initially used variuos online morse code decoder directly but didn't work.Then tried one spectrogram analyser for the wav file then we got the actual morse code of the flag then we used the decoder to get the flag.

Flag: ```bash citadel{1_L0V3_1DM} ```

# The Robot's Trail
You enter a virtual maze, a labyrinth of shifting corridors and endless paths. A guardian robot patrols the floor, leaving a trail behind as it moves. Follow the path it carves, trace its movements carefully, and uncover the key it leads you to. Only by following the robot’s trail can you reach the door to the next floor.

## Solve
So first we need to look at the source code and find the clue of robot.txt clue.Then when we use /robot.txt url we get the next clue to go /file?path=../../etc/passwd url then we get the hint to check out the web server configuration using
/file?path=/var/www/html/config.php:/home/webadmin:/bin/bash url .Then there we get the clue to check out the access logs using /file?path=/var/log/apache2/access.log url. Then we get the hint to look at the environment variables at /proc/self/environ by using /file?path=/proc/self/environ . Then we get to know the secret location as /home/ctf/.secret so we got there to find one of the files in that directory has the flag.

Flag: ```bash citadel{p4th_tr4v3rs4l_m4st3ry_4ch13v3d} ```

# Rotting in the Deep
The floor is quiet, almost unnervingly so – like the Citadel has paused to take your measure. A soft ring of presence settles around the chamber, the kind that marks a true landing: from here, it will ask for more and, in return, grant more. Etched into its surface is a sequence of numbers, worn and faint, as if time itself is eating them away. A whisper from the echoes guides you:

The message lies beneath the surface. Push it three steps forward in the cycle of life, and only then will the words emerge from the void.

## Solve
We just shifted back every digit of the given number by 3 then convert the number to text by using long_to_bytes() function.

Flag: ```bash citadel{br0_r34lly_unr0tt3d_m3_b4ck_t0_l1f3}```

# Coco Conjecture
The door to the next floor is guarded by a figure who calls herself "the dragon CEO". She does not speak of mercy or choice. only of order and efficiency.

To enter the next chamber, you must complete the task presented by her. Complete it exactly as instructed, achieving operational efficiency by her standards, and the path forward will open.

## Solve
 We create a new pythonn file and wrote the code that calculates the collatz steps and created a connection with the server in it then we used the python intepreter python3 command to run this file. Then the code worked to get out the flag.

Flag: ```bash citadel{k1ryu_c0c0_h4s_4_g0_4t_4n_uns0lv3d_m4th3m4t1cs_pr0bl3m}```

# schlagenheim
Your quest continues, but you feel something odd about this room. The only artifact on this floor is a corrupted file held in the hands of a jet-black statue, frozen in the pose of a band mid-performance. The passcode to the next floor is hidden within this piece of music, but it can’t be played, as if the wrong extension has scrambled it.

You must take the corrupted file and repair it to reveal the true code that will unlock the door forward.

## Solve
 We browsed how .wav can be repaired and found that analysing it using a hex editor might work then we opened it in a online hex editor and found that the clue was MIDI so converted this file to a midi file then playing in a midi player got us the flag.

Flag: ```bash citadel{8lackM1D1wa5c00l}```

# XOR Slide
You realise that a previous climber has set up a puzzle in what was otherwise an empty room, blocking the entrance to the next floor on the ceiling. You must slide the blocks forming the pyramid to create a path above.

## Solve
By challenge name itself we got that sliding xor technique needs to used to get to the flag.So we need the code that worked to perform xor operations with the cipher text and the wrapper to get the flag.

Flag: ```bash citadel{pyr4m1d+x0r}```

# The Sound of Music
🗼OSINT pt2: citadweller had a newfound interest in tracking the music they last listened to and posting ratings of new albums on various online platforms.

The flag is hidden in these digital footprints across music platforms and split into three segments. You will need to find all three to uncover the complete code and move on to the next floor.

## Solve
for this we searched across last.fm , spotify, rateyourmusic platforms for user citadweller and found the parts of the flag.

Flag: ```bash citadel{c0mputers_st0pped_exchang1ng_1nf0rmat10n_n_started_shar1ng_st0r1es_n_then_they_were_n0where_t0_be_f0und}```

# Echoes and Pings
You come across the remnants of a fallen corporation and the final network communication ever sent by them.

Allegedly, the message contained an image that predicted the rise of the Citadel. Your task is to uncover what was sent and decode the communication to extract the passcode that will unlock the next floor.

## Solve
We used Wireshark tool to view the .pcap file. among the contents we searched for image as the hint suggested. After browsing found how to identify images by bytes and found a ICMP matches jpg bytes.We caan us a python program to process the ICMP packet to get the image with the flag.

Flag: ```bash citadel{1_r34lly_w4nt_t0_st4y_4t_y0ur_h0us3}```

# The Ripper
The guardian of this floor steps from the shadows. Known only as Jack the Ripper, he watches you carefully. He proclaims himself merciful and hands you a word list to help. He asks you to find the passcode hidden in this hash 
```bash
$2a$04$RNoyoWAcW0StwSri4YN1Eeb2j1gBNKutDOMxsLzfyfSvB/ghMHToa 
```
The word list is your only aid. Only by combining the two correctly can you uncover the key and move on to the next floor. Flag format: 
```bash
citadel{password}
```

## Solve
we identified the hash type by using an online tool and found it is bcrypt hash then we got the flag by doing some terminal operations.

Flag: ```bash citadel{fake_flag_4_fake_pl4y3rs}```

# AetherCorp NetprobeX

You step into a simulation of the past, entering the ruins of AetherCorp, the most ambitious corporation in history, and their creation, NetProbeX, once the most advanced networking tool the world had ever seen. The floor reconstructs the events that led to humanity’s downfall.

Your task is to find the hidden backdoor in NetProbeX, the flaw that triggered the collapse. By uncovering it, you can reverse the damage and retrieve the passcode to advance to the next floor.

## Solve
In order to try to find the loopholes in the website login database, we found SQL injecting could be one of the ways. But none of the usual commands worked , upon browsing we found %0A could be used before each command instead of ' and it worked. So we tried out the UNION SELECT attack along with injecting NULL.Until the no of NULL s exceeded the no of columns which were getting selected by the original SQL query, a particular error was showing error but the page changed when there were 3 Null. We got a list of employees but it didn't provide any useful clue. So then we used ls command to view all the files, we found potential files that could hold the key and then found blacksite_key.dat file and got the flag by reading it.

Flag: ```bash citadel{bl4ck51t3_4cc3ss_gr4nt3d}```

# Feels Like We Only Go Backwards
After finding the backdoor and making your way to the next floor, you step into a chamber awash with shifting colors and swirling echoes, a concert frozen in time. Kevin Parker stands at the center, his riffs bending reality around him. To ascend, you’ll need to join the session on his terms: push your voice further than comfort, align yourself with the number he hides in the haze, and piece together the melody concealed within layers of reverb. Only then will the music open the way upward.

## Solve
We used a IDA to view this file tameimpala. The main idea to proceed with this file to reverse engineering using python code to output.

Flag: ```bash citadel{f0r_0n3_m0r3_h0ur_1_c4n_r4g3}```

# Database Incursion
After your legendary battle with the artist, the virtual world has returned, stretching around you in endless grids and flickering data, you find a rogue data terminal and on careful inspection, you find you’re able to inject rogue structured queries. Using this critical vulnerability, find a way to extract the hidden passcode.

## Solve
So using sql injections as one of the earlier challenges , here we found the working payload as '. then we get the next clue stating managemnt department has the flag so we searched for that empolyee and got his name as Kiwi ansd then we senta final payloa searching for empolyee nnamed Kiwi from Management department and got the flag. 

Flag: ```bash citadel{wh3n_w1ll_y0u_f1nd_0u7_1f_175_5ql_0r_53qu3l?}```

# bratcha
A clear chime rolls through the chamber and a new crest ignites on your badge – a quiet promotion. The outer ring is behind you. From here, the Citadel opens its inner systems, and the locks grow heavier because the keys are worth more. Your answers now carry more weight – and earn more in return. The citadel welcomes you to the inner climb.

Near the gate to the next floor you come across a CAPTCHA verification test, but it has been covered by scratches on the decaying wall and misleading letters stopping you from finding the correct key, all to prove you’re human.

## Solve
 So the image provided to us had overlapping letter which lead to the correct link of pastebin. We needed to run a code to try out all possible combination to get the link and got the flag.

Flag: ```bash citadel{1m_3v3rywh3r3_1m_s0_jul1a}```

# A Memory's a Heavy Burden
You now find yourself in the place where many climbers have been laid to rest. A cold wind moves through the temple grounds, carrying whispers of the departed. Stone lanterns and marble graves reflect Buddhist traditions, their shadows stretching across the frost-covered earth.

The temple rests in the shadow of a very iconic mountain, quiet and imposing. Every detail in the image, the arrangement of the graves, the lanterns, and the lingering scent of incense, holds clues to its true location. You need to uncover the exact coordinates of where you are to move on from here.

Note: round off coordinates to 3 decimal places.

Flag format: citadel{XX.XXX_XXX.XXX}

## Solve
The picture we got simply searching it on web got its coordinates and then enter that in the specified format to get the flag.

Flag: ```bash citadel{35.486_138.699}```

# Case Sensitivity
You step into a constricted floor where every movement and operation is limited. Commands are few, space is tight, and options are restricted.

A guardian looms over the floor, its body shifting like liquid metal, enforcing these constraints. It watches your every move, daring you to make do with what you have and uncover the passcode to the next floor despite the restrictions.

## Solve
Upon connecting to given python intepreter, after trying out various commands and failing we figured out this was a Pyjail and only few selected words we allowed. So while trying print, environ and flag we found the clue that these words were close so we tried different versions of these words and finally figured out that upper cases worked and got the flag using lower() function.

Flag: ```bash citadel{d34th_d035_n07_fr33_y0u_fr0m_7h3_gu17ar15t}```

# Viral Bionic Anomaly
This floor is haunted by a phantom of the past. You encounter a presentation created by the last employee of a forgotten corporation, made just minutes before the Citadel awoke.

Rumor has it that the corporation predicted the rise of the Citadel. Within the slides, a "starter pack" holds the clues you need. Use it to confront the "final boss," a threat trapped inside a macro hidden deep within the presentation, and claim the key to the next floor.

## Solve
I browsed how something can stored within a pptm file and found about macros and opened visual basic to view it and found RunPayload but rying to run failed so i checked the strings given were being decrypted to base32 in the macro. so i followed the program's logic and concatenated all in string in the each function seperately and decoded them into Base32 using cyberchef and then i identify the starting buytes were those of a jpg file so  i attached all the decoded text into one input and used the reder image operation with hex option and managed to get the flag image.  

Flag: ```bash citadel{gr4b_y0ur_l4bubus_m4tch4s_4nd_dub41_ch0c0l4t3s_y0u_4r3_1n_f0r_4_r1d3}```

# Field Day
Deep within the fortified citadel, ancient UNIVAC mainframes hum with classified transmissions. You have spent days infiltrating the Citadel's military grade communication defenses and manage to intercept a FIELDATA transmission encoded onto one of the first methods of storing data. However the data is trapped behind a peculiar digital representation of the FIELDATA encoding, different from the usual 6 bit pairing. Decode the 12 bit transmission to uncover the resistance's secret message.

Attachments: transmission.txt Flag Format: citadel{decodedtransmission}

## Solve
As hinted in the description i found about the UNIVAC 1100 series FIELDATA code. Then we decoded the given transmission data considering the 12 bit pairs using a custom program and got the flag. 

Flag: ```bash citadel{r3b3ll10n$&BU1lt:0nH0p3}```



