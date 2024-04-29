# CQFTooling Refresh Library

## Setup

Get the forked cqf-tooling. This fork adds a missing arg to refresh library and
should be fixed properly at some point:

```
git submodule init
```

## Run build

Run mvn package in the cqf-tooling directory
```
(cd ./support/cqf-tooling && mvn package)
```

NOTE: There are a ton of `ERROR org.opencds.cqf.tooling.operation.ExtractMatBundleOperation - moveAndRenameFiles`, but I just ignore them?

## Run refresh library

In the project root, run the refresh command:

```
java -jar ./support/cqf-tooling/tooling-cli/target/tooling-cli-3.4.0-SNAPSHOT.jar -RefreshLibrary \
  -lp=./input/resources \
  -ini=./ig.ini \
  -fv=4.0.1
```

NOTE: If you want to re-run, you can run this command to reset the library:

```
git checkout -- ./input/resources
```

## Review the XML

Now if you have `jq` and `base64` installed, you can run this to see the ELM

```
jq -cr '.content[] | select(.contentType | contains("application/elm+xml")) | .data' \
  ./input/resources/Library-ExampleLibrary.json \
  | base64 --decode
```

If not, you can look at the ELM XML however you prefer. Here is the XML output, notice the strange namespaces and incorrect case on `library`:

```
<?xml version='1.1' encoding='UTF-8'?>
<Library type="Library" localId="0">
  <wstxns1:identifier xmlns:wstxns1="urn:hl7-org:elm:r1" wstxns1:type="VersionedIdentifier" id="ExampleLibrary" system="http://example.org/fhir/cpg" version="0.1.0"/>
  <wstxns2:schemaIdentifier xmlns:wstxns2="urn:hl7-org:elm:r1" wstxns2:type="VersionedIdentifier" id="urn:hl7-org:elm" version="r1"/>
  <wstxns3:usings xmlns:wstxns3="urn:hl7-org:elm:r1" wstxns3:type="Library$Usings">
    <wstxns3:def>
      <wstxns3:def wstxns3:type="UsingDef" localId="1" localIdentifier="System" uri="urn:hl7-org:elm-types:r1"/>
      <wstxns3:def wstxns3:type="UsingDef" localId="206" locator="3:1-3:26" localIdentifier="FHIR" uri="http://hl7.org/fhir" version="4.0.1">
        <wstxns3:annotation>
          <wstxns3:annotation wstxns3:type="Annotation">
            <wstxns4:s xmlns:wstxns4="urn:hl7-org:cql-annotations:r1" r="206">
              <s>
                <s>
                  <name>{urn:hl7-org:cql-annotations:r1}s</name>
                  <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
                  <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
                  <value>
                    <s>
                      <s></s>
                      <s>using </s>
                    </s>
                  </value>
                  <nil>false</nil>
                  <globalScope>true</globalScope>
                  <typeSubstituted>false</typeSubstituted>
                </s>
                <s>
                  <name>{urn:hl7-org:cql-annotations:r1}s</name>
                  <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
                  <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
                  <value>
                    <s>
                      <s>
                        <name>{urn:hl7-org:cql-annotations:r1}s</name>
                        <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
                        <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
                        <value>
                          <s>
                            <s>FHIR</s>
                          </s>
                        </value>
                        <nil>false</nil>
                        <globalScope>true</globalScope>
                        <typeSubstituted>false</typeSubstituted>
                      </s>
                    </s>
                  </value>
                  <nil>false</nil>
                  <globalScope>true</globalScope>
                  <typeSubstituted>false</typeSubstituted>
                </s>
                <s>
                  <name>{urn:hl7-org:cql-annotations:r1}s</name>
                  <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
                  <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
                  <value>
                    <s>
                      <s> version '4.0.1'</s>
                    </s>
                  </value>
                  <nil>false</nil>
                  <globalScope>true</globalScope>
                  <typeSubstituted>false</typeSubstituted>
                </s>
              </s>
            </wstxns4:s>
          </wstxns3:annotation>
        </wstxns3:annotation>
      </wstxns3:def>
    </wstxns3:def>
  </wstxns3:usings>
  <wstxns5:includes xmlns:wstxns5="urn:hl7-org:elm:r1" wstxns5:type="Library$Includes">
    <wstxns5:def>
      <wstxns5:def wstxns5:type="IncludeDef" localId="207" locator="5:1-5:35" localIdentifier="FHIRHelpers" path="http://hl7.org/fhir/FHIRHelpers" version="4.0.1">
        <wstxns5:annotation>
          <wstxns5:annotation wstxns5:type="Annotation">
            <wstxns6:s xmlns:wstxns6="urn:hl7-org:cql-annotations:r1" r="207">
              <s>
                <s>
                  <name>{urn:hl7-org:cql-annotations:r1}s</name>
                  <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
                  <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
                  <value>
                    <s>
                      <s></s>
                      <s>include </s>
                    </s>
                  </value>
                  <nil>false</nil>
                  <globalScope>true</globalScope>
                  <typeSubstituted>false</typeSubstituted>
                </s>
                <s>
                  <name>{urn:hl7-org:cql-annotations:r1}s</name>
                  <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
                  <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
                  <value>
                    <s>
                      <s>
                        <name>{urn:hl7-org:cql-annotations:r1}s</name>
                        <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
                        <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
                        <value>
                          <s>
                            <s>FHIRHelpers</s>
                          </s>
                        </value>
                        <nil>false</nil>
                        <globalScope>true</globalScope>
                        <typeSubstituted>false</typeSubstituted>
                      </s>
                    </s>
                  </value>
                  <nil>false</nil>
                  <globalScope>true</globalScope>
                  <typeSubstituted>false</typeSubstituted>
                </s>
                <s>
                  <name>{urn:hl7-org:cql-annotations:r1}s</name>
                  <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
                  <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
                  <value>
                    <s>
                      <s> version </s>
                      <s>'4.0.1'</s>
                    </s>
                  </value>
                  <nil>false</nil>
                  <globalScope>true</globalScope>
                  <typeSubstituted>false</typeSubstituted>
                </s>
              </s>
            </wstxns6:s>
          </wstxns5:annotation>
        </wstxns5:annotation>
      </wstxns5:def>
    </wstxns5:def>
  </wstxns5:includes>
  <wstxns7:contexts xmlns:wstxns7="urn:hl7-org:elm:r1" wstxns7:type="Library$Contexts">
    <wstxns7:def>
      <wstxns7:def wstxns7:type="ContextDef" localId="211" locator="7:1-7:15" name="Patient"/>
    </wstxns7:def>
  </wstxns7:contexts>
  <wstxns8:statements xmlns:wstxns8="urn:hl7-org:elm:r1" wstxns8:type="Library$Statements">
    <wstxns8:def>
      <wstxns8:def wstxns8:type="ExpressionDef" localId="209" locator="7:1-7:15" name="Patient" context="Patient">
        <wstxns8:expression wstxns8:type="SingletonFrom" localId="210">
          <wstxns8:operand wstxns8:type="Retrieve" localId="208" locator="7:1-7:15" dataType="{http://hl7.org/fhir}Patient" templateId="http://hl7.org/fhir/StructureDefinition/Patient"/>
        </wstxns8:expression>
      </wstxns8:def>
      <wstxns8:def wstxns8:type="ExpressionDef" localId="213" locator="9:1-9:22" name="Testing" context="Patient" accessLevel="Public">
        <wstxns8:expression wstxns8:type="Literal" localId="214" locator="9:19-9:22" valueType="{urn:hl7-org:elm-types:r1}Boolean" value="true"/>
        <wstxns8:annotation>
          <wstxns8:annotation wstxns8:type="Annotation">
            <wstxns9:s xmlns:wstxns9="urn:hl7-org:cql-annotations:r1" r="213">
              <s>
                <s>
                  <name>{urn:hl7-org:cql-annotations:r1}s</name>
                  <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
                  <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
                  <value r="214">
                    <s>
                      <s></s>
                      <s>define </s>
                      <s>"Testing"</s>
                      <s>: </s>
                      <s>true</s>
                    </s>
                  </value>
                  <nil>false</nil>
                  <globalScope>true</globalScope>
                  <typeSubstituted>false</typeSubstituted>
                </s>
              </s>
            </wstxns9:s>
          </wstxns8:annotation>
        </wstxns8:annotation>
      </wstxns8:def>
    </wstxns8:def>
  </wstxns8:statements>
  <wstxns10:annotation xmlns:wstxns10="urn:hl7-org:elm:r1">
    <wstxns10:annotation wstxns10:type="CqlToElmInfo" translatorVersion="3.9.0" translatorOptions="EnableAnnotations,EnableLocators,DisableListDemotion,DisableListPromotion" signatureLevel="None"/>
    <wstxns10:annotation wstxns10:type="CqlToElmError" message="An operand identifier [reference] is hiding another identifier of the same name." errorType="semantic" errorSeverity="warning"/>
    <wstxns10:annotation wstxns10:type="CqlToElmError" message="The function FHIRHelpers.ToInterval has multiple overloads and due to the SignatureLevel setting (None), the overload signature is not being included in the output. This may result in ambiguous function resolution at runtime, consider setting the SignatureLevel to Overloads or All to ensure that the output includes sufficient information to support correct overload selection at runtime." errorType="semantic" errorSeverity="warning"/>
    <wstxns10:annotation wstxns10:type="CqlToElmError" message="The function FHIRHelpers.ToInterval has multiple overloads and due to the SignatureLevel setting (None), the overload signature is not being included in the output. This may result in ambiguous function resolution at runtime, consider setting the SignatureLevel to Overloads or All to ensure that the output includes sufficient information to support correct overload selection at runtime." errorType="semantic" errorSeverity="warning"/>
    <wstxns10:annotation wstxns10:type="CqlToElmError" message="An operand identifier [reference] is hiding another identifier of the same name." errorType="semantic" errorSeverity="warning"/>
    <wstxns10:annotation wstxns10:type="CqlToElmError" message="An operand identifier [reference] is hiding another identifier of the same name." errorType="semantic" errorSeverity="warning"/>
    <wstxns10:annotation wstxns10:type="Annotation">
      <wstxns11:s xmlns:wstxns11="urn:hl7-org:cql-annotations:r1" r="213">
        <s>
          <s>
            <name>{urn:hl7-org:cql-annotations:r1}s</name>
            <declaredType>org.hl7.cql_annotations.r1.Narrative</declaredType>
            <scope>jakarta.xml.bind.JAXBElement$GlobalScope</scope>
            <value>
              <s>
                <s></s>
                <s>library ExampleLibrary version '0.1.0'</s>
              </s>
            </value>
            <nil>false</nil>
            <globalScope>true</globalScope>
            <typeSubstituted>false</typeSubstituted>
          </s>
        </s>
      </wstxns11:s>
    </wstxns10:annotation>
  </wstxns10:annotation>
</Library>
```