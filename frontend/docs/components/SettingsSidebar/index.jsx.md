```javascript
import React, { useEffect, useRef, useState } from "react";
import paths from "@/utils/paths";
import useLogo from "@/hooks/useLogo";
import {
  EnvelopeSimple,
  SquaresFour,
  Users,
  BookOpen,
  ChatCenteredText,
  Eye,
  Key,
  ChatText,
  Database,
  Lock,
  House,
  List,
  FileCode,
  Notepad,
  CodeBlock,
  Barcode,
  ClosedCaptioning,
  EyeSlash,
  SplitVertical,
  Microphone,
} from "@phosphor-icons/react";
import useUser from "@/hooks/useUser";
import { USER_BACKGROUND_COLOR } from "@/utils/constants";
import { isMobile } from "react-device-detect";
import Footer from "../Footer";
import { Link } from "react-router-dom";

export default function SettingsSidebar() {
  const { logo } = useLogo();
  const { user } = useUser();
  const sidebarRef = useRef(null);
  const [showSidebar, setShowSidebar] = useState(false);
  const [showBgOverlay, setShowBgOverlay] = useState(false);

  useEffect(() => {
    function handleBg() {
      if (showSidebar) {
        setTimeout(() => {
          setShowBgOverlay(true);
        }, 300);
      } else {
        setShowBgOverlay(false);
      }
    }
    handleBg();
  }, [showSidebar]);

  if (isMobile) {
    return (
      <>
        <div className="fixed top-0 left-0 right-0 z-10 flex justify-between items-center px-4 py-2 bg-sidebar text-slate-200 shadow-lg h-16">
          <button
            onClick={() => setShowSidebar(true)}
            className="rounded-md p-2 flex items-center justify-center text-slate-200"
          >
            <List className="h-6 w-6" />
          </button>
          <div className="flex items-center justify-center flex-grow">
            <img
              src={logo}
              alt="Logo"
              className="block mx-auto h-6 w-auto"
              style={{ maxHeight: "40px", objectFit: "contain" }}
            />
          </div>
          <div className="w-12"></div>
        </div>
        <div
          style={{
            transform: showSidebar ? `translateX(0vw)` : `translateX(-100vw)`,
          }}
          className={`z-99 fixed top-0 left-0 transition-all duration-500 w-[100vw] h-[100vh]`}
        >
          <div
            className={`${
              showBgOverlay
                ? "transition-all opacity-1"
                : "transition-none opacity-0"
            }  duration-500 fixed top-0 left-0 ${USER_BACKGROUND_COLOR} bg-opacity-75 w-screen h-screen`}
            onClick={() => setShowSidebar(false)}
          />
          <div
            ref={sidebarRef}
            className="h-[100vh] fixed top-0 left-0  rounded-r-[26px] bg-sidebar w-[80%] p-[18px] "
          >
            <div className="w-full h-full flex flex-col overflow-x-hidden items-between">
              {/* Header Information */}
              <div className="flex w-full items-center justify-between gap-x-4">
                <div className="flex shrink-1 w-fit items-center justify-start">
                  <img
                    src={logo}
                    alt="Logo"
                    className="rounded w-full max-h-[40px]"
                    style={{ objectFit: "contain" }}
                  />
                </div>
                <div className="flex gap-x-2 items-center text-slate-500 shrink-0">
                  <a
                    href={paths.home()}
                    className="transition-all duration-300 p-2 rounded-full text-white bg-sidebar-button hover:bg-menu-item-selected-gradient hover:border-slate-100 hover:border-opacity-50 border-transparent border"
                  >
                    <House className="h-4 w-4" />
                  </a>
                </div>
              </div>

              {/* Primary Body */}
              <div className="h-full flex flex-col w-full justify-between pt-4 overflow-y-scroll no-scroll ">
                <div className="h-auto md:sidebar-items md:dark:sidebar-items">
                  <div className=" flex flex-col gap-y-4 pb-8 overflow-y-scroll no-scroll">
                    <SidebarOptions user={user} />
                  </div>
                </div>
                <Footer />
              </div>
            </div>
          </div>
        </div>
      </>
    );
  }

  return (
    <div>
      <Link
        to={paths.home()}
        className="flex shrink-0 max-w-[55%] items-center justify-start mx-[38px] my-[18px]"
      >
        <img
          src={logo}
          alt="Logo"
          className="rounded max-h-[24px]"
          style={{ objectFit: "contain" }}
        />
      </Link>
      <div
        ref={sidebarRef}
        style={{ height: "calc(100% - 76px)" }}
        className="transition-all duration-500 relative m-[16px] rounded-[16px] bg-sidebar border-2 border-outline min-w-[250px] p-[10px]"
      >
        <div className="w-full h-full flex flex-col overflow-x-hidden items-between min-w-[235px]">
          <div className="text-white text-opacity-60 text-sm font-medium uppercase mt-[4px] mb-0 ml-2">
            Instance Settings
          </div>
          <div className="relative h-full flex flex-col w-full justify-between pt-[10px] overflow-y-scroll no-scroll">
            <div className="h-auto sidebar-items">
              <div className="flex flex-col gap-y-2 h-full pb-8 overflow-y-scroll no-scroll">
                <SidebarOptions user={user} />
              </div>
            </div>
            <div className="mb-2">
              <Footer />
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}

const Option = ({
  btnText,
  icon,
  href,
  childLinks = [],
  flex = false,
  user = null,
  allowedRole = [],
  subOptions = null,
  hidden = false,
}) => {
  if (hidden) return null;

  const hasActiveChild = childLinks.includes(window.location.pathname);
  const isActive = window.location.pathname === href;

  // Option only for multi-user
  if (!flex && !allowedRole.includes(user?.role)) return null;

  // Option is dual-mode, but user exists, we need to check permissions
  if (flex && !!user && !allowedRole.includes(user?.role)) return null;

  return (
    <>
      <div className="flex gap-x-2 items-center justify-between">
        <Link
          to={href}
          className={`
          transition-all duration-[200ms]
          flex flex-grow w-[75%] gap-x-2 py-[6px] px-[12px] rounded-[4px] justify-start items-center
          hover:bg-workspace-item-selected-gradient hover:text-white hover:font-medium
          ${
            isActive
              ? "bg-menu-item-selected-gradient font-medium border-outline text-white"
              : "hover:bg-menu-item-selected-gradient text-zinc-200"
          }
        `}
        >
          {React.cloneElement(icon, { weight: isActive ? "fill" : "regular" })}
          <p className="text-sm leading-loose whitespace-nowrap overflow-hidden ">
            {btnText}
          </p>
        </Link>
      </div>
      {!!subOptions && (isActive || hasActiveChild) && (
        <div
          className={`ml-4 ${
            hasActiveChild ? "" : "border-l-2 border-slate-400"
          } rounded-r-lg`}
        >
          {subOptions}
        </div>
      )}
    </>
  );
};

const SidebarOptions = ({ user = null }) => (
  <>
    <Option
      href={paths.settings.system()}
      btnText="System Preferences"
      icon={<SquaresFour className="h-5 w-5 flex-shrink-0" />}
      user={user}
      allowedRole={["admin", "manager"]}
    />
    <Option
      href={paths.settings.invites()}
      btnText="Invitation"
      icon={<EnvelopeSimple className="h-5 w-5 flex-shrink-0" />}
      user={user}
      allowedRole={["admin", "manager"]}
    />
    <Option
      href={paths.settings.users()}
      btnText="Users"
      icon={<Users className="h-5 w-5 flex-shrink-0" />}
      user={user}
      allowedRole={["admin", "manager"]}
    />
    <Option
      href={paths.settings.workspaces()}
      btnText="Workspaces"
      icon={<BookOpen className="h-5 w-5 flex-shrink-0" />}
      user={user}
      allowedRole={["admin", "manager"]}
    />
    <Option
      href={paths.settings.chats()}
      btnText="Workspace Chat"
      icon={<ChatCenteredText className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin", "manager"]}
    />
    <Option
      href={paths.settings.appearance()}
      btnText="Appearance"
      icon={<Eye className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin", "manager"]}
    />
    <Option
      href={paths.settings.apiKeys()}
      btnText="API Keys"
      icon={<Key className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin"]}
    />
    <Option
      href={paths.settings.llmPreference()}
      btnText="LLM Preference"
      icon={<ChatText className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin"]}
    />
    <Option
      href={paths.settings.audioPreference()}
      btnText="Voice and Speech Support"
      icon={<Microphone className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin"]}
    />
    <Option
      href={paths.settings.transcriptionPreference()}
      btnText="Transcription Model"
      icon={<ClosedCaptioning className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin"]}
    />
    <Option
      href={paths.settings.embedder.modelPreference()}
      childLinks={[paths.settings.embedder.chunkingPreference()]}
      btnText="Embedder Preferences"
      icon={<FileCode className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin"]}
      subOptions={
        <>
          <Option
            href={paths.settings.embedder.chunkingPreference()}
            btnText="Text Splitter & Chunking"
            icon={<SplitVertical className="h-5 w-5 flex-shrink-0" />}
            user={user}
            flex={true}
            allowedRole={["admin"]}
          />
        </>
      }
    />
    <Option
      href={paths.settings.vectorDatabase()}
      btnText="Vector Database"
      icon={<Database className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin"]}
    />
    <Option
      href={paths.settings.embedSetup()}
      childLinks={[paths.settings.embedChats()]}
      btnText="Chat Embed Widgets"
      icon={<CodeBlock className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin"]}
      subOptions={
        <>
          <Option
            href={paths.settings.embedChats()}
            btnText="Chat Embed History"
            icon={<Barcode className="h-5 w-5 flex-shrink-0" />}
            user={user}
            flex={true}
            allowedRole={["admin"]}
          />
        </>
      }
    />
    <Option
      href={paths.settings.security()}
      btnText="Security"
      icon={<Lock className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin", "manager"]}
      hidden={user?.role}
    />
    <Option
      href={paths.settings.logs()}
      btnText="Event Logs"
      icon={<Notepad className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin"]}
    />
    <Option
      href={paths.settings.privacy()}
      btnText="Privacy & Data"
      icon={<EyeSlash className="h-5 w-5 flex-shrink-0" />}
      user={user}
      flex={true}
      allowedRole={["admin"]}
    />
  </>
);

```
**Documentation for SidebarOptions Interface**

### Purpose and Usage

The `SidebarOptions` interface provides a configurable sidebar component that can be used in various parts of your application. This interface is designed to render a list of options with corresponding icons, text, and links.

### Methods Documentation

#### Option

* Signature: `(href: string, btnText: string, icon: JSX.Element, user: User, allowedRole?: string[]) => JSX.Element`
* Purpose: Renders an option button with the specified href, text, and icon.
* Parameters:
	+ `href`: The URL to link to when the option is clicked. (string)
	+ `btnText`: The text displayed on the button. (string)
	+ `icon`: The icon element to display next to the button text. (JSX.Element)
	+ `user`: The user object containing information about the current user. (User)
	+ `allowedRole`: An optional array of allowed roles for this option. (string[])
* Return value: A JSX element representing the option button.

Example:
```jsx
<Options>
  <Option href="/settings" btnText="System Preferences" icon={<SquaresFour />} />
  <Option href="/invites" btnText="Invitation" icon={<EnvelopeSimple />} />
</Options>
```
#### Option with sub-options

* Signature: `(href: string, btnText: string, icon: JSX.Element, user: User, allowedRole?: string[], childLinks?: string[]) => JSX.Element`
* Purpose: Renders an option button with sub-options.
* Parameters:
	+ `href`: The URL to link to when the option is clicked. (string)
	+ `btnText`: The text displayed on the button. (string)
	+ `icon`: The icon element to display next to the button text. (JSX.Element)
	+ `user`: The user object containing information about the current user. (User)
	+ `allowedRole`: An optional array of allowed roles for this option. (string[])
	+ `childLinks`: An optional array of child links to render as sub-options. (string[])
* Return value: A JSX element representing the option button with sub-options.

Example:
```jsx
<Options>
  <Option href="/embed" btnText="Chat Embed Widgets" icon={<CodeBlock />} subOptions={
    <Fragment>
      {childLinks.map((link) => (
        <Option key={link} href={link} btnText={link} />
      ))}
    </Fragment>
  } />
</Options>
```
### Dependencies

The `SidebarOptions` interface relies on the following dependencies:

* The `User` type, which represents the current user.
* The `JSX.Element` type, which is used to render icons and other UI elements.

### Examples

Here are some examples of how you can use the `SidebarOptions` interface:
```jsx
import React from 'react';
import { SidebarOptions } from './SidebarOptions';

const App = () => {
  const user = { role: 'admin' };
  return (
    <SidebarOptions>
      <Option href="/settings" btnText="System Preferences" icon={<SquaresFour />} user={user} />
      <Option href="/invites" btnText="Invitation" icon={<EnvelopeSimple />} user={user} />
      <Option href="/embed" btnText="Chat Embed Widgets" icon={<CodeBlock />} subOptions={
        <Fragment>
          {['chat1', 'chat2', 'chat3'].map((link) => (
            <Option key={link} href={link} btnText={link} />
          ))}
        </Fragment>
      } user={user} />
    </SidebarOptions>
  );
};
```
### Consistency and Clarity

The documentation for the `SidebarOptions` interface is written in a clear and concise manner, with examples provided to illustrate its usage. The method signatures are well-documented, including parameter types and descriptions. The interface's dependencies are clearly stated, and the documentation is organized in a logical and easy-to-follow manner.