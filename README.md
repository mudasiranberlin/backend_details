# backend_details

# 1. Importing Packages

# import mongoose,{Schema} from "mongoose";
# Used to connect and work with MongoDB.

mongoose → complete library
Schema → blueprint/template for data
# JWT
import jwt from "jsonwebtoken"

Used to create login tokens.

When user logs in:

# Instead of asking for username/password every time, the user sends the token.

# bcrypt
Used to encrypt passwords.
Example:

Password:123456
Stored in database:

$2b$10$ksjdhfksjdhfkjsdhf...

# This is called hashing.

# Pre Save Middleware
# userSchema.pre("save", async function() {
Runs BEFORE saving user.

# Check Password Changed
# if (!this.isModified("password")) return

# Meaning:

# "If password wasn't changed, stop here."

# Example: Changing username only: user.username="newName"

# No need to hash password again.

# Hash Password     this.password = await bcrypt.hash(this.password,10)

# Example: Before: 123456   After:  $2b$10$hdfkjsdhfkjsdhf...

# The 10 is the salt rounds.   More rounds: 10    = More security but slower.

# Password Checking Method:

# Password Checking Method

userSchema.methods.isPasswordCorrect =
async function(password)
Creates a custom method.

# When user logs in:
email
password
# Need to compare entered password with stored hashed password.

return await bcrypt.compare(
    password,
    this.password
)

Example:  entered 123456   Stored:  $2b$10$hash...

# bcrypt checks if they match.
# return True or false 


# Generate Access Token
userSchema.methods.generateAccessToken=
function()
Creates login token.

# Payload
{
    _id:this._id,
    email:this.email,
    username:this.username,
    fullname:this.fullname
}
Information stored inside token.







