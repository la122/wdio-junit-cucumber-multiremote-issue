# Demo for junit reporter issue with wdio multiremote

## Singleremote

Running `npx wdio wdio.conf.ts` generates a junit report as expected:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<testsuites tests="1" failures="0" errors="0" skipped="0">
  <testsuite name="Demo" timestamp="2026-02-23T12:40:40" time="0.007" tests="1" failures="0" errors="0" skipped="0">
    <properties>
      <property name="specId" value="0"/>
      <property name="featureName" value="Demo"/>
      <property name="capabilities" value="chrome.145_0_7632_77.mac"/>
      <property name="featureFile" value="file://./features/login.feature"/>
    </properties>
    <testcase classname="CucumberJUnitReport-chrome.145_0_7632_77.mac.Demo" name="Three steps" time="0.002">
      <system-out><![CDATA[
✅ Given step 1
✅ When step 2
✅ Then step 3
]]></system-out>
    </testcase>
  </testsuite>
</testsuites>
```

## Multiremote

Running `npx wdio wdio.conf.multiremote.ts` generates a problematic junit report:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<testsuites tests="3" failures="0" errors="0" skipped="0">
  <testsuite name="Three steps" timestamp="2026-02-23T12:39:35" time="0.004" tests="3" failures="0" errors="0" skipped="0">
    <properties>
      <property name="specId" value="0"/>
      <property name="suiteName" value="Three steps"/>
      <property name="capabilities" value=""/>
      <property name="file" value="file://./features/login.feature"/>
    </properties>
    <testcase classname=".login.feature:1:1:_Three_steps" name="Given step 1" time="0.001"/>
    <testcase classname=".login.feature:1:1:_Three_steps" name="When step 2" time="0.001"/>
    <testcase classname=".login.feature:1:1:_Three_steps" name="Then step 3" time="0">
      <system-out><![CDATA[
COMMAND: DELETE /session/undefined - {}
RESULT: {}
]]></system-out>
    </testcase>
  </testsuite>
  <testsuite name="Demo" timestamp="2026-02-23T12:39:35" time="0.007" tests="0" failures="0" errors="0" skipped="0">
    <properties>
      <property name="specId" value="0"/>
      <property name="suiteName" value="Demo"/>
      <property name="capabilities" value=""/>
      <property name="file" value="file://./features/login.feature"/>
    </properties>
  </testsuite>
</testsuites>
```

- There are now 3 tests instead of 1
- Steps are interpreted as test cases
- Steps are not listed in system-out
