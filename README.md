# Scripts
Thresh Script
local myHero = nil
local myHeroPos = nil

function AfterObjectLoopEvent(myHer0)
    myHero = myHer0
    myHeroPos = GetOrigin(myHero)
		DrawText("Thresh Script by IMCOOL.",24,0,0,0xffff0000);
	
	local target = GetCurrentTarget()
	if KeyIsDown(0x20) then 
	    if ValidTarget(target, 1100) then
			if CanUseSpell(myHero, _Q) == READY and GetDistance(GetOrigin(target), GetOrigin(myHero)) < 1100*1100 then
				CastTargetSpell(target, _Q)
			end
			if CanUseSpell(myHero, _E) == READY and GetDistance(GetOrigin(target), GetOrigin(myHero)) < 400*400 then
				CastTargetSpell(target, _E)
			end
	  	end
	end	
end

function ValidTarget(unit, range)
	if GetOrigin(unit) == nil or IsDead(unit) or GetTeam(unit) == GetTeam(myHero) or GetDistance(GetOrigin(unit)) > range*range then return false end
	return true
end

function GetDistance(p1,p2)
	p2 = p2 or myHeroPos
	local dx = p1.x - p2.x
	local dz = (p1.z or p1.y) - (p2.z or p2.y)
	return dx*dx + dz*dz

end
