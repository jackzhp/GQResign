similar stuff:


https://github.com/trongvu/ipa_generator
https://github.com/behrad-kzm/resigner
https://github.com/trongvu/ipa_generator


some explanation

#1. unzip old.ipa
#remove those garbage
## remove old signatures
    rm -rf Payload/{appName}-mobile.app/_CodeSignature
## remove old embedded.mobileprovision
    rm -rf Payload/{appName}-mobile.app/embedded.mobileprovision
## auto generated garbage files    
	find ./ -name ".DS_Store" -depth -exec rm {} \\;
# put into the new embedded.mobileprovision at the place.
   the file usually from apple's website.
# prepare entitlements.plist
	security cms -D -i "Payload/{appName}-mobile.app/embedded.mobileprovision > entitlements_full.plist
    /usr/libexec/PlistBuddy -x -c 'Print:Entitlements' entitlements_full.plist > entitlements.plist
# resign
    codesign -f -s "iPhone Distribution: ITM, OOO" Payload/{appName}-mobile.app --entitlements entitlements.plist
# now we zip                
    zip -r new.ipa Payload

