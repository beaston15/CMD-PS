# CMD-PS

## Command Prompt and Powershell Incident Response

![CMD 1](https://github.com/beaston15/CMD-PS/assets/121417326/f0407752-bc46-4a06-95d8-cafcbc3dde57)

<p>
Using the command "net users", All users are shown with one suspicous user being "ServiceeAccount". 
</p>
<br />

![CMD 2](https://github.com/beaston15/CMD-PS/assets/121417326/14f8df64-f769-4f43-8301-5529094be121)

<p>
Knowing that there is a suspcious user account we can investigate groups, in this case we choose to look into the administrators group using the command "net localgroup adminitrators". ServiceeAccount is shown to be in the administrators group possibly giving this account permissions it should not have.
</p>
<br />

![CMD 3](https://github.com/beaston15/CMD-PS/assets/121417326/087df314-331e-47c3-b07b-a1c9a4ecf3bb)

<p>
Next the "Remote Desktop Users" group is investiaged which shows that the ServiceeAccount user is allowed to logon remotely. At this point the account can be confirmed to be an intruder since it is allowed to be logged in remotely with adminitrators permissions.
</p>
<br />

![CMD 4](https://github.com/beaston15/CMD-PS/assets/121417326/f5932924-147f-4105-a730-af391f4e1d25)

<p>
Now using Powershell with the command "Get-LocalUser -Name ServiceeAccount | Select *", we can get a lot of information about the ServiceeAccount user. The most important detail we might be looking for is the Last Logon date and time to see how active the intruder is.
</p>
<br />

![CMD 5](https://github.com/beaston15/CMD-PS/assets/121417326/9df7eae1-a31a-4fb8-8d6b-68b202d4dd66)

<p>
Lastly we look at scheduled task that the intruder may have made, using the command "Get-ScheduledTask | Where State -eq "Ready"" there is a TaskName of "Persistence" that is suspicious. 
</p>
<br />
