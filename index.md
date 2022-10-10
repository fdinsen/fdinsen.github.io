<script src="https://unpkg.com/launchdarkly-js-client-sdk@2.18.1/dist/ldclient.min.js"></script>

<h1>Hello, World</h1>

<div id="preview" style="display:none"> 
<p>Trunk based development works directly on the trunk (main) branch locally, and when work finished is pushed directly to trunk on shared repo. Larger teams can use feature branches in the same way as Github Flow, but feature branches should be VERY shortlived (a day or two)
Two ways to release: release directly from trunk when new changes (for teams with rapid release). Or with slower release (weekly or monthly), create release branch off of trunk a few days before each release. Creating release branch allows teams to continue working against trunk, without affecting release. If hotfixes necessary, fixed on trunk then merged to release using cherry pick of single commit containing fix. 
 
Since all features pushed to trunk (even unfinished), use feature flagging to turn on/off features. So code can be in production code without being active to customer. Can be selectively turned on for developers. Deployment is when source code is shipped to environment. Release is when deployed feature is toggled available to users. 
Flagging strategies: 
-	Basic toggle: turn feature on or off per environment
-	Targeted: make feature available to certain user segments
-	Rollout: release feature to a gradually increasing percentage of users
Feature flags can be implemented manually using if statements and configuration files for the flags, or using specifically designed platforms (eg. Launch darkly or flagship)</p>

</div>

<script> 
    var clientId = "63441136a896721118acb6ec"; 
    var flagName = "explaination-of-TBD";
    var user = { anonymous: true }; 
    var ldclient = window.LDClient.initialize(clientId, user); 
    
    ldclient.on("ready", function() { 
        document.getElementById("preview").style.display = ldclient.variation(flagName, false) ? "block":"none"; 
    }); 
    ldclient.on("change:" + flagName, function(newVal, prevVal) { 
        document.getElementById("preview").style.display = newVal ? "block":"none"; 
    }); 
</script>